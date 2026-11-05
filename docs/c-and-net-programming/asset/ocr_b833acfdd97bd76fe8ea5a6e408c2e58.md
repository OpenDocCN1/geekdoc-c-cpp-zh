# 3) Out of process mode - Storing session in State Server process

+   1) In this mode, a separate Windows Service runs in a different process that stores the Session.
+   2) This method isolates the Session from the ASP.NET running process. Due to separate process its performance degrades.
+   3) This mode is ideal for scalable and highly available applications.
+   4) Advantages
+      Session data is persisted across application domain recycles. This is achieved by using separate worker process for maintaining state
+      Supports web farm and web garden configuration
+   5) Disadvantages
+      It requires data serializing.
+      It has overhead in encoding View State values
+      Inappropriate for sensitive data
+   6) Session state is held in a process called aspnet_state.exe that runs as a windows service which listens on TCP port 42424 by default. State service can be invoked using services MMC snap-in or by running following net command from command line.
+   7) Configuration Settings

```
<sessionState mode="StateServer"
StateConnectionString="tcpip=127.0.0.1:42424"
sqlConnectionString="data source=127.0.0.1;
user id=RaviW; password=technical"
cookieless="false" timeout="20"/>
```

# 4) Storing session in SQL server

+   1) SQL Server mode is the one in which the Session is stored in SQL Server rather than in the server's memory.
+   2) When the application is stored on multiple server machines, then it is infeasible to use "Inproc" mode as the requests go to any server for processing. Therefore, in this situation, only feasible centralized place to hold the Session is in SQL
+   3) Server which can be accessed by any server during the request process. Though low performance, it is the most secure way of storing Sessions.
+   4) Following is the Code snippet illustrating how values are stored and retrieved for Session.