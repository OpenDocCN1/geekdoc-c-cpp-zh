threads is 1. This is because the Java socket API synchronizes the accept call so only one thread can actually wait on accept. Hence there is no benefit to increasing the number of acceptor threads. If blocking sockets are used, the recommended number of acceptor threads is 20. For the thread pool associated with the HTTP Connector, its Max Pool Size parameter determines the total number of worker threads available.

Figure 15-2 adds an outbound SOAP over HTTP call to the picture. The thread doing the component work ② also performs the HTTP interaction and then resumes the execution of the component work. Upon completion of the component work, thread ② returns the HTTP response to the initial requestor.

# Default JMS Thread Usage

The default thread usage for JMS or SOAP over JMS interactions is shown in Figure 15-3. The service consumer places the inbound request on the JMS queue. A JMS client/session thread (not from one of the thread pools) ① picks up the request and passes it to a worker thread ② from the JMS or SOAP/JMS binding. The worker thread is taken

![](bbox=[0.12, 0.71, 0.95, 0.88])

Figure 15-2: Default Thread Usage for Outbound HTTP Communications