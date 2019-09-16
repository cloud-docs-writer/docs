# Подключение к базе данных в кластере {{ PG }}

{% include [cluster-connect-note](../../_includes/mdb/cluster-connect-note.md) %}

## Аутентификация

{{ PG }}-кластеры {{ mpg-short-name }} поддерживают только шифрованные соединения. Поэтому для подключения к такому кластеру необходим SSL-сертификат. Подготовить все нужные аутентификационные данные можно так:

```bash
$ mkdir ~/.postgresql
$ wget "https://storage.yandexcloud.net/cloud-certs/CA.pem" -O ~/.postgresql/CA.pem
```

О том, как использовать сертификат с помощью `libpq`, читайте в [документации {{ PG }}](https://www.postgresql.org/docs/current/static/libpq-connect.html#LIBPQ-PARAMKEYWORDS).

## Строка подключения

Теперь вы можете подключиться к БД с помощью команды `psql`:

```bash
psql "host=<FQDN хоста БД> \
      port=6432 \
      sslmode=verify-full \
      dbname=<имя базы данных> \
      user=<имя пользователя базы данных>"
```

{% include [see-fqdn-in-console](../../_includes/mdb/see-fqdn-in-console.md) %}

## Автоматический выбор хоста-мастера


### С библиотекой libpq
Чтобы гарантированно подключиться к хосту-мастеру, укажите FQDN всех хостов кластера в аргументе `host` и передайте параметр `target_session_attrs=read-write`. Этот параметр поддерживается библиотекой `libpq` начиная с [версии 10](https://www.postgresql.org/docs/10/static/libpq-connect.html):

```bash
psql "host=<FQDN хоста 1>,<FQDN хоста 2>,<FQDN хоста 3> \
      port=6432 \
      sslmode=verify-full \
      dbname=<имя базы данных> \
      user=<имя пользователя базы данных> \
      target_session_attrs=read-write"
```

Чтобы обновить версию библиотеки, которую использует утилита `psql`:

* Для дистрибутивов Linux на основе Debian — установите пакет `postgresql-client-10` (например, через [apt-репозиторий](https://www.postgresql.org/download/linux/ubuntu/)).

* Для ОС, использующих RPM-пакеты, дистрибутив {{ PG }} доступен в [yum-репозитории](https://yum.postgresql.org/).


Адреса всех хостов в кластере БД можно найти на странице нужного кластера в консоли управления.


### С драйвером, поддерживающим только один хост

Если ваш драйвер для подключения к базе данных не позволяет передавать несколько хостов в строке подключения (например,
[pgx в Go](https://github.com/jackc/pgx)), вы можете подключаться на специальный хост вида `c-<идентификатор кластера>.rw.{{ dns-zone }}`.


Это доменное имя всегда указывает на текущий мастер в кластере. Например, для кластера с идентификатором `c9qash3nb1v9ulc8j9nm` к мастеру можно подключиться так:

```bash
$ psql "host=c-c9qash3nb1v9ulc8j9nm.rw.mdb.yandexcloud.net \
      port=6432 \
      sslmode=verify-full \
      dbname=<имя базы данных> \
      user=<имя пользователя базы данных>"
```


