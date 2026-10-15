7. Open the Default.aspx.cs file and add the System.ServiceModel namespace, as shown in the following code snippet:

```
using System.ServiceModel;
```

Using the WCF service requires adding the reference of the WCF service in the application in which you want to call the service, and generating the proxy code for the client and a .config file, which we explore next.

# Adding the Reference of WCF service

After creating a WCF client, you can add the reference of the WCF service to the client. In our case, we add a reference of a WCF service by adding the .svc file of the service in the MyFirstWCFClient website. For this, right-click the MyFirstWCFClient website in Solution Explorer and select the Add Service Reference option. This opens the Add Service Reference dialog box.

In the Address text box of the Add Service Reference dialog box, enter the URL of your WCF service and click the Go button. You can see your WCF service in the Services box, and a list of its methods in the Operations box. Now, change the name of the service reference from ServiceReference1 to MyWCFServiceReference and click the OK button, as shown in Figure 19.37:

![](bbox=[0.23, 0.31, 0.77, 0.635])

Figure 19.37: Showing the Add Service Reference Dialog Box

> NOTE
> You need to build the application before adding the service reference in the application.

Now, you need generate proxy code using the svcutil.exe file.

# Generating the Proxy Code

The .NET Framework 3.5 and 4.0 Server Development Kit (SDK) provides an approach to build a client-side proxy (the code that is automatically generated from the metadata provided by the service) through the Svcutil.exe file. Using the Svcutil.exe file, you can generate a .cs file that represents the proxy code for the client and a .config file that contains the client's configuration details. Let's perform the following steps to use the Svcutil.exe file:

+   1. Open the Visual Studio 2010 Command Prompt and type the following command:

```
svcutil.exe /language:cs /out:MyWCFClient.cs /config:MyWCFClient.config http://localhost:6485/MyFirstWCFService/Service.svc
```

+   2. Press the ENTER key. The preceding command generates two files, MyWCFClient.cs and MyWCFClient.config, as shown in Figure 19.38: