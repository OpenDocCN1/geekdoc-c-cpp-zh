it sends back the result, and the work process becomes free again to take a new request.

![](bbox=[0.1476, 0.1589, 0.8567, 0.4667])

**Figure 2.4** Dispatcher and Work Process

Work processes are not dedicated to any user session. They can take requests from any user. For example, as shown in Figure 2.4, User 1 executes a report. This request is assigned to Work Process 1 by the dispatcher. Work Process 1 processes the request and sends the result back to User 1.

At this point, if User 2 makes a request, the dispatcher can assign it to Work Process 1, because that work process is free to take a new request. If User 1 makes a new request while Work Process 1 is processing the request from User 2, then the dispatcher will simply assign the User 1 request to Work Process 2. If a new request is made by either User 1 or User 2 while both Work Process 1 and Work Process 2 are busy, then the dispatcher will assign this task to the next available work process.

You can see how the work process statuses change by opening Transaction SM50 (see Figure 2.5). If you run any program and check Transaction SM50, you’ll notice that the request is processed by a dialog work process (DIA) with a RUNNING status. The work processes that are free to take requests have a WAITING status.