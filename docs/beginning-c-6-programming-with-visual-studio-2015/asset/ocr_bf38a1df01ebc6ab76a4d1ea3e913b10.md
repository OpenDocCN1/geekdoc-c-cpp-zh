much more difficult to implement in web services. You can also integrate with IIS features such as IIS security.

+   - Executable — You can host a WCF service in any application type that you can create in .NET, such as console applications, Windows Forms applications, and WPF applications.
+   - Windows service — You can host a WCF service in a Windows service, which means that you can use the useful features that Windows services provide. This includes automatic startup and fault recovery.
+   - Windows Activation Service (WAS) — Designed specifically to host WCF services, WAS is basically a simple version of IIS that you can use where IIS is not available.

Two of the options in the preceding list — IIS and WAS — provide useful features for WCF services such as activation, process recycling, and object pooling. If you use either of the other two hosting options, the WCF service is said to be self-hosted. You will occasionally self-host services for testing purposes, but there can be very good reasons for creating self-hosted production-grade services. For example, you could be in a situation where you're not allowed to install a web server on the computer on which your service should run. This might be the case if the service runs on a domain controller or if the local policy of your organization simply prohibits running IIS. In this case you can host the service in a Windows service and it will work every bit as well as it would otherwise.

# WCF PROGRAMMING

Now that you have covered all the basics, it is time to get started with some code. In this section you'll start by looking as a simple web server–hosted WCF service and a console application client. After looking at the structure of the code created, you'll learn about the basic structure of WCF services and client applications. Then you will look at some key topics in a bit more detail:

+   - Defining WCF service contracts
+   - Self-hosted WCF services

# TRY IT OUT A Simple WCF Service and Client: Ch22Ex01Client

+   1. Create a new WCF Service Application project called Ch22Ex01 in the directory C:\BegVCSharp\Chapter22.
+   2. Add a console application called Ch22Ex01Client to the solution.
+   3. On the Build menu, click Build Solution.
+   4. In the Ch22Ex01Client project, right click References in the Solution Explorer and select Add Service Reference.
+   5. In the Add Service Reference dialog box, click Discover.
+   6. When the development web server has started and information about the WCF service has been loaded, expand the reference to look at its details. Notice that there are two methods in the service: GetData and GetDataUsingDataContract.