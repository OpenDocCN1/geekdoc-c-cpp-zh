That’s the basic idea: your App Engine code is always written as a bunch of HTTP request handlers/servlets. If you want to do computation on the server, you create something that tells the server how to generate the request, and you’re in business. There’s nothing special about how you write task implementations— they’re just event handlers. In fact, you can create events that send requests to the same URLs used by human users. There is really no difference between a task implementation and any other handler. The reporting handler that we wrote for cron tasks works perfectly as a task implementation. We could also write tasks that submit chat messages, exactly the way a user would, simply by enqueuing a task that performs a request on the submit-chat URL with the right parameters.

# Creating Tasks

What do the tasks look like from your code? As we said, they’re simple objects that tell the server how to create an HTTP request.

So if we want to send an email (as we did in the previous section in order to send a daily report on chat room usage), we define a task that has one parameter—the email address that the report should be sent to. That’s it. Since the URL for our report generation was /report, that will be the URL of the request. We implement the report generator to handle a GET request: so when we build the task, we make it a GET. We don’t need to implement the handler, because we already did. The cron job generates a completely normal GET, so our task can use the same handler—it just needs to generate the same basic GET.

If we want users to be able to request a usage report in our chat service, we add a button to our user interface that generates a GWT remote procedure call. The call invokes the generateReport method:

Download w2/ReportingChat/src/com/google/appengine/.../chat/server/ChatUserServiceImpl.java

```
```java
@Override
public void generateReport(String address) {
    TaskOptions task = method(TaskOptions.Builder.withMethod.GET).param("to", address);
    QueueFactory.getDefaultQueue().add(task);
}
```
```

There’s something odd about this code. In App Engine, we submit a task by creating a TaskOptions object describing the task. But we don’t create one explicitly. Instead, we call a static method on the class com.google.appengine.api.labs.taskqueue.TaskOptions.Builder. To create a GET task, we call the method called method in the pack-