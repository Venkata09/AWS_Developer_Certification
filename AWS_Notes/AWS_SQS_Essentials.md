
If **ChangeMessageVisibility** is used to request more time when the visibility timeout is not enough.

**ReceiveMessageWaitTimeSeconds** is used to set the short/long polling .

When creating the queue (For all message receptions ) :

aws sqs create-queue --queue-name myQueue --attributes "ReceiveMessageWaitTimeSeconds=20"
When receiving message ( For specific reception) :

aws sqs receive-message --queue-url $queueurl --wait-time-seconds 20

For the WaitTimeSeconds parameter of ReceiveMessage, a value set between 1 and 20 has priority over any value set for the queue attribute ReceiveMessageWaitTimeSeconds.source

The time value set in ReceiveMessage has priority over anything set by ReceiveMessageWaitTimeSeconds attribute of the Queue.
