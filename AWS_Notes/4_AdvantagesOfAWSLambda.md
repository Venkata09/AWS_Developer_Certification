# Using Java with AWS Lambda has very powerful features. 

##### Java has better performance and consistency when you compare it with other languages for the same time window — although this may change based on what you do within your function.

## Synchronous Execution
**This may be a bit personal, but as someone who wrote with both Java and Node.js for AWS Lambda, dealing with callbacks is troublesome, and the async nature of Node.js does not feel right. If concurrency is what you need, then you can either deal with it in your application or write smaller functions.**

## Tooling Support
**with the rise of serverless, tooling for Java will be better. Proportional to the maturity of the language, Java has lots of great tooling support, including IDEs (IntelliJ IDEA, Eclipse, etc.), dependency management, and build tools (Maven, Gradle,…).**

## The Issue With Cold Starts
**Cold starts cause latency when a new container is created underneath. 
If your functions are granular, you will probably not going to experience this a lot. However, if your traffic is unpredictable or sparse and if you offer latency SLAs, this can cause you some trouble. 
Because of the nature of the Java language, Java functions experience more latency than other languages. For now, there is no exact solution to this problem, but there are ways to reduce them until then. With Java 9 supporting the Oracle JDK’s nice features like AOT (Ahead of Time Compilation), hopefully coming soon to AWS Lambda, we hope that AWS will make use of it and maybe other creative solutions to reduce the cold start times for Java.**
