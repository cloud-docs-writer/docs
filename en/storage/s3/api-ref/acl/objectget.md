# objectGetAcl method

Returns the access control list for an object.

## Request {#request}

```
GET /{bucket}/{key}?acl HTTP/1.1
```

### Path parameters {#path-parameters}

| Parameter | Description |
| ----- | ----- |
| `bucket` | Name of the bucket. |
| `key` | Object key. |

### Query parameters {#request-params}

| Parameter | Description |
| ----- | ----- |
| `acl` | Required parameter that indicates the type of operation. |

### Headers {#request-headers}

Use the necessary [common request headers](../common-request-headers.md) in requests.

## Response {#response}

### Headers {#response-headers}

Responses can only contain [common response headers](../common-response-headers.md).

### Data schema {#response-scheme}

The structure of the returned data is described in [ACL XML schema](xmlscheme.md).

### Response codes {#response-codes}

For a list of possible responses, see [{#T}](../response-codes.md).

