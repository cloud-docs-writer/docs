# Deleting clusters

{% note important %}

Backups of deleted clusters are stored for seven days.

{% endnote %}

{% list tabs %}

- Management console
  1. Open the folder page in the management console.
  1. Select **{{ mrd-name }}**.
  1. Click ![image](../../_assets/options.svg) for the necessary cluster and select **Delete**.
  1. In the window that opens, check **Delete cluster** and click **Delete**.

- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  To delete a cluster, run the command:

  ```
  $ yc managed-redis cluster delete <cluster name or ID>
  ```

  The cluster name and ID can be requested with a [list of clusters in the folder](cluster-list.md).

{% endlist %}

