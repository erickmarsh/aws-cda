
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
TODO

S3 API
============================
TODO


CloudFormation
====================
TODO

ElasticBeanstalk
=======================
TODO


