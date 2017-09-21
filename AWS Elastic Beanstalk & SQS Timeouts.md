I have been reading about Worker Environments in AWS Elastic Beanstalk. I found all the timeouts confusing at first, so I share my findings here.

The instances in your Worker Environment have a demon that reads messages from an SQS Queue. That queue has a Default Visibility Timeout and Message Retention Period. 
In addition, the Elastic Beanstalk Worker Configuration has its own Visibility Timeout and Retention Period in addition to a Connection Timeout, Error Visibility Timeout and Inactivity Timeout. 


The process works like this (see diagram below). 
1. The SQS demon polls the queue. When it reads a message, it sets the Visibility Timeout overriding the queue's Default Visibility Timeout. 
1. The demon then checks if the message is older than the Retention Period. 
1. If it is, it explicitly deletes the message, effectively overriding the queue's Message Retention Period. In other words, the Worker Environment's Visibility Timeout and Retention Period replace the queue's Default Visibility Timeout and Message Retention Period respectively.

Assuming the demon finds a message that has not exceeded the Retention Period, it does an HTTP POST (Delivering message to your application) with the message in the body to your running application which should be listening on 127.0.0.1:80. 
If the demon cannot create a connection to your application within the Connection Timeout it sets the message's visibility to the Error Visibility Timeout. The message will be retied after the Error Visibility Timeout.

If the demon can create a connection, it waits for a response. If the Inactivity Timeout is exceeded before the demon receives a response, it aborts the request and sets the message's Visibility to the Error Visibility Timeout. The message will be retied after the Error Visibility Timeout.

Note that your entire run does need to complete within the Inactivity Timeout (max 30 mins). Each time your application sends data the counter is reset. In other words you can hold the HTTP connection open for longer than 30 minutes by streaming data back in small increments. You could extend this up to the Visibility Timeout (max 12 hours). While SQS allows you to reset the visibility timeout, Elastic Beanstalk does provide the receipt handle to your code.

At this point we have addressed all seven of the timeouts you can configure (2 on the queue and 5 in worker configuration), but we came this far so let's see this through to completion. If the demon receives a response from your application, it checks the return code. If the response indicates success (i.e. 200) it explicitly deletes the message from SQS and the process completes. If the response indicates failure, the demon sets the message's Visibility to the Error Visibility Timeout. The message will be retied after the Error Visibility Timeout.





**Understand Amazon SQS visibility timeouts.** Visibility timeout is a period of time during which Amazon SQS prevents other components from receiving and processing a message because another component is already processing it. By default, the message visibility timeout is set to 30 seconds, and the maximum that it can be is 12 hours.
