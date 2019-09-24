# Static website in {{ objstorage-full-name }}

To host a static website in Object Storage:

1. [Create a bucket with public access](#create-public-bucket)
1. [Configure the website's home page and the error page](#index-and-error)
1. [Configure use of your own domain](#connect-your-domain)
1. [Upload the website files](#upload-files)

## 1. Create a public bucket {#create-public-bucket}

To create a bucket for static website files:

1. Go to the Yandex.Cloud [management console]({{ link-console-main }}) and select the folder where you want to perform the operations.

1. On the folder page, click **Create resource** and select **Bucket**.

1. In the **Name** field, enter the bucket name (for instance, `www.example.com`). The bucket name will be used in the website domain name: `https://www.example.com.{{ s3-web-host }}`.

   The name must meet the following requirements:

   {% include [bucket-name-reqs](../../_includes/bucket-name-reqs.md) %}

   {% note info %}

   If you plan to use your own domain for the website, the bucket name must exactly match the name of your domain, and this must be a third-level or higher domain.

   {% endnote %}

1. Specify the maximum size of the bucket in GB.

1. Choose **Public** access to the bucket.

1. Click **Create bucket**.

## 2. Configure the website's home page and the error page {#index-and-error}

You should upload and configure the index page and error page. To do this:

1. Create the following files on your computer:
   * `index.html` with the text `Hello world!`.
The file content will be displayed when accessing the website's home page.
   * `error.html` with the text `Error!`.
The file content will appear in the website responses with `4ххх` errors.
1. Go to your bucket's page, open the **Objects** tab, and click **Upload**. In the window that opens, select the created files and click the confirmation button.
1. Click **Upload**.
1. Open the **Website** tab on your bucket page.
1. Select **Hosting**.
1. In the **Home page** field, specify `index.html`.
1. In the **Error page** field, specify `error.html`.
1. Click **Save**.
1. Make sure the website's home page opens. To do this, connect to the website through a browser via a link like `https://{bucket-name}.{{ s3-web-host }}`.
1. Make sure the error page opens. To do this, connect to the website through a browser via a link like `https://{bucket-name}.{{ s3-web-host }}/error-check`.

## 3. Configure use of your own domain {#connect-your-domain}

To use your own domain for a website:

- Make sure the bucket name is exactly the same as the domain name. This must be a third-level or higher domain (for example, `www.example.com`).
- Create a CNAME (Canonical Name) record at your DNS provider or on your own DNS server.

{% note info %}

The website is accessible only over HTTP, for instance, `http://www.example.com` or `http://www.example.com.{{ s3-web-host }}`.

{% endnote %}

The instructions below describe how to configure an external DNS service using as an example [reg.ru](https://www.reg.ru/) for domain names `www.example.com.{{ s3-web-host }}` and `www.example.com`:

1. Go to the bucket page and open the **Website** tab in the [management console]({{ link-console-main }}) and find the website address.
1. Log in to the control panel of the external DNS service. Go to the [list of your domains](https://www.reg.ru/user/domain_list) and click on the required domain name.
1. Follow the **Zone management** link in the **Domain management** section.
1. Create a CNAME record with the following field values:
   * **Subdomain**: `www`.
   * **Canonical name**:  website address with a dot at the end (for instance, `www.example.com).{{ s3-web-host }}.`.
1. Wait 15-20 minutes for DNS record changes to take effect. The waiting time may differ for your DNS service.

## 4. Upload the website files to the bucket {#upload-files}

After you configure and test the website's availability, upload the remaining files that are necessary for website operation. Do that via the [management console]({{ link-console-main }}), [API](../../storage/s3/api-ref/object/upload.md), or one of the available [tools for working with {{ objstorage-name }}](../../storage/instruments/).

