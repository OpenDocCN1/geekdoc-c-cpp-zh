# State Server Mode

In this mode session data is stored in separate server.

# SQL Server Mode

In this session is stored in the database. It is a secure mode.

# Custom Mode

Generally under session data is stored in inproc, Sql Server, State server, etc. If you store session data with other new techniques then provide ASP.NET.

# Application

Application State is a server side management state. It is also called application level state management. In this mainly store user activity in server memory and store application event shown in Global.asax file.

Their are three types of applications in ASP.NET.

# Application_Start

This event begins with domain start.

```
Void Application_Start(object sender, eventargs e)
{
	Application["appstartmessage"] = "Welcome to csharp Corner Developer Community";
}
```