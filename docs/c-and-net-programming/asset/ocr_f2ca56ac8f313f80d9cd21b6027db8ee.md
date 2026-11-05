+   - 2) It supports "customization for session state through the state provider.
+   - 3) The contents are kept in session state variables using the IIS.

# 12) Disadvantage of the Session State

The state variables are present in the memory until explicitly removed or replaced due to which the server performance degrades.

# 13) Session object

+   1) Session object is used to store state specific information per client basis. It is specific to particular user.
+   2) Session data persists for the duration of user session. Session's data can be stored on web server in different ways.
+   3) Session state in ASP.NET can be configured in different ways based on various parameters including scalability, maintainability and availability
+   4) Configuring Session State,

Session state can be configured using the <session State> section in the application's web.config file as mentioned below.

```
<sessionState mode = "<'inproc' | 'sqlserver' | 'stateserver'>
cookieless = <'true' | 'false'>
timeout = <positive integer indicating the session timeout in minutes>
sqlconnectionstring =
    <SQL connection string that is only used in the SQLServer mode>
server =
    <The server name that is only required when the mode is State Server>
port =
    <The port number that is only required when the mode is State Server>
```

Where Settings Details are as explained below,

# i) Cookie less

This setting takes a Boolean value of either true or false to indicate whether the Session is a cookie less one.

# ii) Timeout