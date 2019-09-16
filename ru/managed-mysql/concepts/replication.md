# Репликация

В кластерах {{ mmy-name }} используется асинхронная построчная репликация: результат запроса на запись отражается на репликах кластера с задержкой относительно мастера. Подробнее о построчной репликации читайте в [документации СУБД](https://dev.mysql.com/doc/refman/5.7/en/replication-rbr-usage.html).

{% include [non-replicating-hosts](../../_includes/mdb/non-replicating-hosts.md) %}

Также включены глобальные идентификаторы транзакций ([GTID](https://dev.mysql.com/doc/refman/5.7/en/replication-gtids-concepts.html)), которые помогают поддерживать консистентность данных между хостами кластера.