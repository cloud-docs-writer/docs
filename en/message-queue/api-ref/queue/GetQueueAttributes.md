# GetQueueAttributes

Method for getting attributes for the specified queue.

If the queue name ends with the `.fifo` suffix, the type of the requested queue is [FIFO](../../concepts/queue.md#fifo-queues).

## Request {#request}

### Request parameters {#request-parameters}

| Parameter | Type | Required parameter | Description |
| ----- | ----- | ----- | ----- |
| `QueueUrl` | **string** | Yes | URL of a queue. |
| `Attributes.N.*` | [list of](#attributes) | No | List of queue attributes. |

#### Attributes {#attributes}

Queue attributes. Attributes are sent as a list. For more information about passing list parameters, see [Using the API](../index.md#array-parameters).

```
Attribute.N.Name (attribute)
Attribute.N.Value (attribute value)
```

| Attribute | Description |
| ----- | ----- |
| `All` | Returns all attributes of a queue. |
| `ApproximateNumberOfMessages` | Returns the approximate number of enqueued messages that can be received. |
| `ApproximateNumberOfMessagesDelayed` |  Returns the approximate number of messages in the queue that are delayed and not available for reading immediately. |
| `ApproximateNumberOfMessagesNotVisible` | Returns the approximate number of messages that are in flight: they have been sent to a client but have not yet been deleted or have not yet reached the end of their [visibility timeout](../../concepts/visibility-timeout.md). |
| `CreatedTimestamp` | Returns the time when the queue was created in seconds (epoch time). |
| `DelaySeconds` |  The number of seconds to [delay the message](../../concepts/delay-queues.md) from being available for processing. |
| `LastModifiedTimestamp` | Returns the time when the queue was last changed in seconds  (epoch time). |
| `MaximumMessageSize` | Returns the maximum message size in bytes. |
| `MessageRetentionPeriod` | Returns the length of time, in seconds, for which a message is retained. |
| `ReceiveMessageWaitTimeSeconds` | Returns the length of time, in seconds, for which the [ReceiveMessage](../message/ReceiveMessage) action waits for a message to arrive. |
| `VisibilityTimeout` | Returns the [visibility timeout](../../concepts/visibility-timeout.md) for the queue, specified in seconds. |

#### FIFO queue attributes {#fifo-path-parameters}

| Attribute | Description |
| ----- | ----- |
| `FifoQueue` | Returns whether the queue is [FIFO](../../concepts/queue.md#fifo-queues). To determine whether a queue is FIFO, check whether its name ends with the `.fifo` suffix. |
| `ContentBasedDeduplication` | Returns whether [content-based deduplication](../../concepts/deduplication.md#content-based-deduplication) is enabled for the queue. |

#### Non-supported attributes

| Attribute | Type | Description |
| ----- | ----- | ----- |
| `RedrivePolicy` | **string** | Not supported in Yandex Message Queue. |
| `KmsMasterKeyId` | **string** | Not supported in Yandex Message Queue. |
| `KmsDataKeyReusePeriodSeconds` | **string** | Not supported in Yandex Message Queue. |

## Response {#response}

### Successful response fields {#response-parameters}

| Field | Type | Description |
| ----- | ----- | ----- |
| `Attributes.N.*` | **array** | Array of queue attributes. |

### GetQueueAttributes errors {#errors}

For a list of errors that are common to all methods, see the section [{#T}](../common-errors.md).

| HTTP code | Error ID | Description |
| ----- | ----- | ----- |
| 400 | `InvalidAttributeName` | The attribute name is invalid. |

## Sample request {#request-example}

```
Action=GetQueueAttributes
&Version=2012-11-05
&QueueUrl=https://message-queue.api.cloud.yandex.net/b1g8ad42m6he1ooql78r/dj600000000000le07ol/sample-queue
&AttributeName.1=All
```

For more information about forming requests, see [General format of an API request](../index.md#api-request).

## Sample response {#response-example}

```xml
<GetQueueAttributesResponse>
    <GetQueueAttributesResult>
        <Attribute>
            <Name>ApproximateNumberOfMessages</Name>
            <Value>0</Value>
        </Attribute>
        <Attribute>
            <Name>ApproximateNumberOfMessagesDelayed</Name>
            <Value>0</Value>
        </Attribute>
        <Attribute>
            <Name>ApproximateNumberOfMessagesNotVisible</Name>
            <Value>0</Value>
        </Attribute>
        <Attribute>
            <Name>CreatedTimestamp</Name>
            <Value>1548345183</Value>
        </Attribute>
        <Attribute>
            <Name>DelaySeconds</Name>
            <Value>0</Value>
        </Attribute>
        <Attribute>
            <Name>MaximumMessageSize</Name>
            <Value>262144</Value>
        </Attribute>
        <Attribute>
            <Name>MessageRetentionPeriod</Name>
            <Value>345600</Value>
        </Attribute>
        <Attribute>
            <Name>ReceiveMessageWaitTimeSeconds</Name>
            <Value>0</Value>
        </Attribute>
        <Attribute>
            <Name>VisibilityTimeout</Name>
            <Value>30</Value>
        </Attribute>
    </GetQueueAttributesResult>
    <ResponseMetadata>
        <RequestId>a69769e7-d07122f-147f09c0-e1f9d20-2e4fd5bae005ef4e6d639f7946b42bde</RequestId>
    </ResponseMetadata>
</GetQueueAttributesResponse>
```

