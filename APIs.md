
EC2 API Methods 
================================
http://docs.aws.amazon.com/AWSEC2/latest/APIReference/OperationList-query.html

AMI
-------------
|Name|Description|
|---|---|
|CreateImage | Creates an Amazon EBS-backed AMI from an Amazon EBS-backed instance that is either running or stopped. |
|CopyImage | Initiates the copy of an AMI from the specified source region to the current region. You specify the destination region by using its endpoint when making the request. |


EBS
-----------------
|Name|Description|
|---|---|
|CreateVolume | Creates an EBS volume that can be attached to an instance in the same Availability Zone. The volume is created in the regional endpoint that you send the HTTP request to. For more information see Regions and Endpoints. |
|AttachVolume | Attaches an EBS volume to a running or stopped instance and exposes it to the instance with the specified device name. The ID of the EBS volume. The volume and instance must be within the same Availability Zone. |
|CreateSnapshot | Creates a snapshot of an EBS volume and stores it in Amazon S3. You can use snapshots for backups, to make copies of EBS volumes, and to save data before shutting down an instance. |
|CopySnapshot | Copies a point-in-time snapshot of an EBS volume and stores it in Amazon S3. You can copy the snapshot within the same region or from one region to another. You can use the snapshot to create EBS volumes or Amazon Machine Images (AMIs). The snapshot is copied to the regional endpoint that you send the HTTP request to.
|DeleteSnapshot | Detaches an EBS volume from an instance. Make sure to unmount any file systems on the device within your operating system before detaching the volume. Failure to do so can result in the volume becoming stuck in the busy state while detaching. If this happens, detachment can be delayed indefinitely until you unmount the volume, force detachment, reboot the instance, or all three. If an EBS volume is the root device of an instance, it can't be detached while the instance is running. To detach the root volume, stop the instance first.

Elastic IP Address
-------------------------
|Name|Description|
|---|---|
|AllocateAddress | Acquires an Elastic IP address. An Elastic IP address is for use either in the EC2-Classic platform or in a VPC. For more information, see Elastic IP Addresses in the Amazon Elastic Compute Cloud User Guide. |
|AssociateAddress | Associates an Elastic IP address with an instance or a network interface.
|DisassociateAddress | |
|ReleaseAddress | |



SNS API
========================== 
|Name|Description|
|---|---|
|CreateTopic |Creates a topic to which notifications can be published. Users can create at most 100,000 topics. For more information, see http://aws.amazon.com/sns. This action is idempotent, so if the requester already owns a topic with the specified name, that topic's ARN is returned without creating a new topic. |
|Subscribe | Prepares to subscribe an endpoint by sending the endpoint a confirmation message. To actually create a subscription, the endpoint owner must call the ConfirmSubscription action with the token from the confirmation message. Confirmation tokens are valid for three days. |
|ConfirmSubscription | Verifies an endpoint owner's intent to receive messages by validating the token sent to the endpoint by an earlier Subscribe action. If the token is valid, the action creates a new subscription and returns its Amazon Resource Name (ARN). This call requires an AWS signature only when the AuthenticateOnUnsubscribe flag is set to "true". |
|Publish | Sends a message to all of a topic's subscribed endpoints. When a messageId is returned, the message has been saved and Amazon SNS will attempt to deliver it to the topic's subscribers shortly. The format of the outgoing message to each subscribed endpoint depends on the notification protocol. |
|DeleteTopic | Deletes a topic and all its subscriptions. Deleting a topic might prevent some messages previously sent to the topic from being delivered to subscribers. This action is idempotent, so deleting a topic that does not exist does not result in an error. |

SQS API
============================
|Name|Description|
|---|---|
|CreateQueue | Creates a new queue, or returns the URL of an existing one. When you request CreateQueue, you provide a name for the queue. To successfully create a new queue, you must provide a name that is unique within the scope of your own queues.
|ListQueues | Returns a list of your queues. The maximum number of queues that can be returned is 1000. If you specify a value for the optional QueueNamePrefix parameter, only queues with a name beginning with the specified value are returned.
|AddPermission | Adds a permission to a queue for a specific principal. This allows for sharing access to the queue. When you create a queue, you have full control access rights for the queue. Only you (as owner of the queue) can grant or deny permissions to the queue. For more information about these permissions, see Shared Queues in the Amazon SQS Developer Guide.
|SendMessage | Delivers a message to the specified queue. With Amazon SQS, you now have the ability to send large payload messages that are up to 256KB (262,144 bytes) in size. To send large payloads, you must use an AWS SDK that supports SigV4 signing. To verify whether SigV4 is supported for an AWS SDK, check the SDK release notes. |
|ReceiveMessage | Retrieves one or more messages, with a maximum limit of 10 messages, from the specified queue. Long poll support is enabled by using the WaitTimeSeconds parameter. For more information, see Amazon SQS Long Poll in the Amazon SQS Developer Guide.
|DeleteMessage | Deletes the specified message from the specified queue. You specify the message by using the message's receipt handle and not the message ID you received when you sent the message. Even if the message is locked by another reader due to the visibility timeout setting, it is still deleted from the queue. If you leave a message in the queue for longer than the queue's configured retention period, Amazon SQS automatically deletes it. You can receive a deleted message if delete has not propogated. Make sure your system can handle this |
|PurgeQueue | Deletes the messages in a queue specified by the queue URL. Can take up to 60 seconds
|DeleteQueue | Deletes the queue specified by the queue URL, regardless of whether the queue is empty. If the specified queue does not exist, Amazon SQS returns a successful response. Can take 60 seconds |

DynamoDb API
============================
CreateTable
-----------------
The CreateTable operation adds a new table to your account. In an AWS account, table names must be unique within each region. That is, you can have two tables with same name if you create the tables in different regions.CreateTable is an asynchronous operation. Upon receiving a CreateTable request, DynamoDB immediately returns a response with a TableStatus of CREATING. After the table is created, DynamoDB sets the TableStatus to ACTIVE. You can perform read and write operations only on an ACTIVE table.You can optionally define secondary indexes on the new table, as part of the CreateTable operation. If you want to create multiple tables with secondary indexes on them, you must create the tables sequentially. Only one table with secondary indexes can be in the CREATING state at any given time.

DeleteTable
--------------------
The DeleteTable operation deletes a table and all of its items. After a DeleteTable request, the specified table is in the DELETING state until DynamoDB completes the deletion. If the table is in the ACTIVE state, you can delete it. If a table is in CREATING or UPDATING states, then DynamoDB returns a ResourceInUseException. If the specified table does not exist, DynamoDB returns a ResourceNotFoundException. If table is already in the DELETING state, no error is returned.

GetItem
-------------------
The GetItem operation returns a set of attributes for the item with the given primary key. If there is no matching item, GetItem does not return any data and there will be no Item element in the response.

DeleteItem
-------------------
Deletes a single item in a table by primary key. You can perform a conditional delete operation that deletes the item if it exists, or if it has an expected attribute value. In addition to deleting an item, you can also return the item's attribute values in the same operation, using the ReturnValues parameter.Unless you specify conditions, the DeleteItem is an idempotent operation; running it multiple times on the same item or attribute does not result in an error response. Conditional deletes are useful for deleting items only if specific conditions are met. If those conditions are met, DynamoDB performs the delete. Otherwise, the item is not deleted.

UpdateItem
---------------------------
Edits an existing item's attributes, or adds a new item to the table if it does not already exist. You can put, delete, or add attribute values. You can also perform a conditional update on an existing item (insert a new attribute name-value pair if it doesn't exist, or replace an existing name-value pair if it has certain expected attribute values). You can also return the item's attribute values in the same UpdateItem operation using the ReturnValues parameter.

Query
--------------------
A Query operation uses the primary key of a table or a secondary index to directly access items from that table or index.Use the KeyConditionExpression parameter to provide a specific value for the partition key. The Query operation will return all of the items from the table or index with that partition key value. You can optionally narrow the scope of the Query operation by specifying a sort key value and a comparison operator in KeyConditionExpression. You can use the ScanIndexForward parameter to get results in forward or reverse order, by sort key.Queries that do not return results consume the minimum number of read capacity units for that type of read operation.If the total number of items meeting the query criteria exceeds the result set size limit of 1 MB, the query stops and results are returned to the user with the LastEvaluatedKey element to continue the query in a subsequent operation. Unlike a Scan operation, a Query operation never returns both an empty result set and a LastEvaluatedKey value. LastEvaluatedKey is only provided if you have used the Limit parameter, or if the result set exceeds 1 MB (prior to applying a filter).

Scan
-----------------
The Scan operation returns one or more items and item attributes by accessing every item in a table or a secondary index. To have DynamoDB return fewer items, you can provide a FilterExpression operation.If the total number of scanned items exceeds the maximum data set size limit of 1 MB, the scan stops and results are returned to the user as a LastEvaluatedKey value to continue the scan in a subsequent operation. The results also include the number of items exceeding the limit. A scan can result in no table data meeting the filter criteria. By default, Scan operations proceed sequentially; however, for faster performance on a large table or secondary index, applications can request a parallel Scan operation by providing the Segment and TotalSegments parameters. For more information, see Parallel Scan in the Amazon DynamoDB Developer Guide.

BatchWriteItem
--------------------
The BatchWriteItem operation puts or deletes multiple items in one or more tables. A single call to BatchWriteItem can write up to 16 MB of data, which can comprise as many as 25 put or delete requests. Individual items to be written can be as large as 400 KB.BatchWriteItem cannot update items. To update items, use the UpdateItem action. 

The individual PutItem and DeleteItem operations specified in BatchWriteItem are atomic; however BatchWriteItem as a whole is not. If any requested operations fail because the table's provisioned throughput is exceeded or an internal processing failure occurs, the failed operations are returned in the UnprocessedItems response parameter. You can investigate and optionally resend the requests. Typically, you would call BatchWriteItem in a loop. Each iteration would check for unprocessed items and submit a new BatchWriteItem request with those unprocessed items until all items have been processed. 
*Note* that if none of the items can be processed due to insufficient provisioned throughput on all of the tables in the request, then BatchWriteItem will return a ProvisionedThroughputExceededException.


DynamoDB API Errors
================================
InternalServerError
-------------------------
An error occurred on the server side.

HTTP Status Code: 500


ItemCollectionSizeLimitExceededException
-------------------------
An item collection is too large. This exception is only returned for tables that have one or more local secondary indexes.

HTTP Status Code: 400

ProvisionedThroughputExceededException
------------------------------
Your request rate is too high. The AWS SDKs for DynamoDB automatically retry requests that receive this exception. Your request is eventually successful, unless your retry queue is too large to finish. Reduce the frequency of requests and use exponential backoff. For more information, go to Error Retries and Exponential Backoff in the Amazon DynamoDB Developer Guide.

HTTP Status Code: 400

ResourceNotFoundException
-------------------------------
The operation tried to access a nonexistent table or index. The resource might not be specified correctly, or its status might not be ACTIVE.

HTTP Status Code: 400

IncompleteSignature
-------------------------------
The request signature does not conform to AWS standards.

HTTP Status Code: 400

InternalFailure
-------------------------------
The request processing has failed because of an unknown error, exception or failure.

HTTP Status Code: 500

InvalidAction
-------------------------------
The action or operation requested is invalid. Verify that the action is typed correctly.

HTTP Status Code: 400

InvalidClientTokenId
-------------------------------
The X.509 certificate or AWS access key ID provided does not exist in our records.

HTTP Status Code: 403

InvalidParameterCombination
-------------------------------
Parameters that must not be used together were used together.

HTTP Status Code: 400

InvalidParameterValue
-------------------------------
An invalid or out-of-range value was supplied for the input parameter.

HTTP Status Code: 400

InvalidQueryParameter
-------------------------------
The AWS query string is malformed or does not adhere to AWS standards.

HTTP Status Code: 400

MalformedQueryString
-------------------------------
The query string contains a syntax error.

HTTP Status Code: 404

MissingAction
-------------------------------
The request is missing an action or a required parameter.

HTTP Status Code: 400

MissingAuthenticationToken
-------------------------------
The request must contain either a valid (registered) AWS access key ID or X.509 certificate.

HTTP Status Code: 403

MissingParameter
-------------------------------
A required parameter for the specified action is not supplied.

HTTP Status Code: 400

OptInRequired
-------------------------------
The AWS access key ID needs a subscription for the service.

HTTP Status Code: 403

RequestExpired
-------------------------------
The request reached the service more than 15 minutes after the date stamp on the request or more than 15 minutes after the request expiration date (such as for pre-signed URLs), or the date stamp on the request is more than 15 minutes in the future.

HTTP Status Code: 400

ServiceUnavailable
-------------------------------
The request has failed due to a temporary failure of the server.

HTTP Status Code: 503

Throttling
-------------------------------
The request was denied due to request throttling.

HTTP Status Code: 400

ValidationError
-------------------------------
The input fails to satisfy the constraints specified by an AWS service.

HTTP Status Code: 400





S3 API
============================
REST API

Authentication
------------------------
**HTTP Authorization header** 
Using the HTTP Authorization header is the most common method of authenticating an Amazon S3 request. All of the Amazon S3 REST operations (except for browser-based uploads using POST requests) require this header.

**Query string parameters**
ou can use a query string to express a request entirely in a URL. In this case, you use query parameters to provide request information, including the authentication information. Because the request signature is part of the URL, this type of URL is often referred to as a presigned URL. You can use presigned URLs to embed clickable links, which can be valid for up to seven days, in HTML.

PUT Bucket
-----------------
Creates a new Bucket

POST Object & Put Object
---------------------------
Uploads a new file to S3
Requires write access
Can send MD5 to ensure upload is successful

DELETE Object
-----------------------------
The DELETE operation removes the null version (if there is one) of an object and inserts a delete marker, which becomes the current version of the object. If there isn't a null version, Amazon S3 does not remove any objects.


CloudFormation
====================
TODO

ElasticBeanstalk
=======================
TODO


