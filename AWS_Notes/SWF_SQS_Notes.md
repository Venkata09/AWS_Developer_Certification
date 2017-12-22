##SQS Simple Queue Service

Loosely decouples the resources

it is a scalable messaging system

Queues are used to store messages that travel between different components of architecture

each queue can have unlimited messages, and you can create unlimited queues

components are called workers, thy keep polling the queue

allows individual resource to scale up based on load

SQS guarantees delivery atleast once. So there can me more than 1 duplicate messages

messages can be upto 256kb in size. can also attach instructions to access larger messages in dynamodb or s3

64kb is 1 billable message unit

Lifecycle: 1. Component 1 sends message to Q and the message is redundantly distributed across SQS server. 2. When component2 is ready, it retrieves and messages becomes invisible from queue for a period of visibility timeout. 3. Component2 deletes the message after successfully processing the message

Short polling (default) : polls only a subset of SQS servers. Continuous short polling to get all messages. Each short poll is charged, there might be empty messages and be charged

Long polling: reduces cost as reduces number of empty messages

Long polling does not return a response till a message is available or till the long poll times out

Long polling has maximum timeout of 20 seconds

delay queue(0sec to 12 hours): amount of time to delay the first message

message retention period (1 minute to 14 days, default is 4 days): amount of time message will remain in queue if not deleted

default visibility timeout 30 seconds ; can be upto 12 hours. ChangeMessageVisibility

receive message wait time: If set > 0, then long polling is enabled.

Upto 120k inflight messages

SQS does not guarantee the delivery order of the messages

if order is important, then sequencing info can be embedded in the message

each message has a globally unique id which sqs returns when message is delivered to the queue

Dead letter queues are offered where one SQS can get messages from another SQS

SQS fanning out can be done using SNS topics where messages can be fanned out to other SQS queues

SQS Does not guarantee first in first out

can send upto 10 attributes as metadata on each message. As name-type-value triplets

Queue names are limited to 80 characters, should be unique within an aws account

AWS might delete a queue if there is no activity for 30 days

Messages cannot be shared between queues in different regions

Common API

ChangeMessageVisibility : change visibility by worker
ChangeMessageVisibility : for upto 10 messages
SetQueueAttribues/GetQueueAttributes
VisibilityTimeout attribute to change default visibility timeout
ReceiveMessageWaitTimeSeconds (>0 for long polling) max is 20 seconds
DelaySeconds
DeleteMessageBatch: deletes multiple message
SentTimestamp
GetQueueURL : returns URL for an existing queue
CreateQueue, ListQueue, SendMessage, SendMessageBatch...
PurgeQueue to delete all messages in the queue
SQS service access point URL : http://sqs..amazonaws.com

##Simple Work Flow Services

Each step is a task, similar to SQS

Task coordination and state management service

A workflow can consist of human events, unlike SQS

A workflow can last upto 1 year

It guarantees the order in which activities/tasks occurs

Domains

domain helps to determine the scope of work
multiple workflows can live inside a domain
workflows cannot interact with workflows in other domains
workers and deciders

Activity workers - process that performs an activity in the workflow
Activity workers poll SWF for new tasks that they need to perform
Activity workers will perform the task and report back to SWF.
Workers can be servers on EC2 or on premise, or humans
workers can be run behind firewall
Activity task is a task assigned to a worker

Decision task tells the decider that the state has changed. It allows decider to decide next activity.

Decision task occurs whenever the state of workflow changes ex when task completes

SQS vs SWF

SQS has best effort message order and potentially has duplicates
SWF guarantees execution order and uses deciders for next instructions
SQS messages live upto 14 days, SWF workflow can last upto 1 year
SWF allows synchronous or asynchronous distributed processing
SWF is task oriented, whereas SQS is message oriented
Limits

10000 workflow and activity types
100 SWF domains
100000 open executions in a domain
SWF workflow can last maximum for 1 year
