# Getting started with {{ mch-short-name }}


To use the service, create a cluster and connect to a DBMS:

1. All you need to create a database cluster is a folder in Yandex.Cloud that you are allowed to access. If you already have a folder in Yandex.Cloud, open the page of that folder in the management console. If there is no folder yet, create one:

    {% include [create-folder](../_includes/create-folder.md) %}

2. You can connect to DB clusters from both inside and outside of the Cloud:

    1. To connect to a DB cluster from inside the Cloud, create a VM in the same network as the DB cluster (based on [Linux](../compute/quickstart/quick-create-linux.md) or [Windows](../compute/quickstart/quick-create-windows.md))

    2. To enable connection to a cluster over the internet, request external IP addresses for hosts when creating the cluster.

1. In the management console, select the folder where you want to create a DB cluster.


1. Click **Create resource** and select **Cluster{{ CH }}**.

1. Set the cluster parameters and click **Create cluster**. This process is described in detail in [{#T}](operations/cluster-create.md).

1. When the cluster is ready, its status on the {{ mch-name }} dashboard will change to **RUNNING**.

1. To connect to the DB server, you need an SSL certificate. Download it:

    ```bash
    $ wget "https://storage.yandexcloud.net/cloud-certs/CA.pem"
    ```

1. Send a request specifying the path to the received SSL certificate, database attributes, and the request text in urlencoded format:

    ```
    $ curl --cacert <path to the SSL certificate> \
         -H "X-ClickHouse-User: <DB username>" \
         -H "X-ClickHouse-Key: <DB user password>" \
         'https://<host address>:8443/?database=<DB name>&query=SELECT%20now ()'
    ```


