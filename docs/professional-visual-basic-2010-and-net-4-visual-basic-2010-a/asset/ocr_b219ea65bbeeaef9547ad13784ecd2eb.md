Currently, you can create five types of service:

+   - ASP.NET Web role — This is a standard Web service that will host an ASP.NET application in the cloud. You would include one of these to provide a visible user interface to your cloud.
+   - MVC 2 Web role — This is a Web service that will host an application built using the ASP.NET MVC Framework.
+   - WCF Web role — This is a Web service that includes one or more WCF services. You would include one of these to provide Web Services in your application.
+   - Worker role — This is a nonvisible application that will run within your cloud. Typically, these are background tasks needed by your Web application, or calculation services. For example, you might have a worker role to transfer orders to a fulfillment service, or a worker role that processes data to determine trends.
+   - CGI Web role — This is a Web service that is designed to run Web applications written in PHP, Python, Ruby, or other non-ASP.NET languages.

For now, add a single Web role to the application, called ToDoWeb. After adding the Web role, set the name by clicking the pencil icon. This will be the user interface for the application.

The Web role looks and works exactly like an ASP.NET application: You get an initial default.aspx page, and it includes a web.config file and the jQuery script libraries. The one difference is the addition of a WebRole.vb file. This file contains two methods:

+   - OnStart — This method overrides the method in the base class RoleEntryPoint. This is called when the role is initialized within the Azure fabric, and could be thought of as analogous to a constructor. You can perform any initialization required at this point. The method should return true if the role is ready to participate in the Azure environment, or false if something prevents it from doing so. For example, you could connect to your data sources here. If they were not available for some reason, you could set OnStart to false to prevent the Web role from initializing.
+   - RoleEnvironmentChanging — This is an event the Azure environment may call when some change has been made to the configuration of a running instance. This enables your application to reload the configuration settings and act accordingly.

After a brief grind or two of your hard drive, you should see something like Figure E-13 in the Solution Explorer. In addition to the ASP.NET application, you have the Windows Azure project that consists of the single Web role you added, and two configuration files.

The two configuration files identify the port that the Web role will listen on, as well as the size and number of instances that will run. You can edit these files by hand, but it is much easier to use Visual Studio to edit them. Right-click on ToDoWeb in the Roles folder and select Properties to configure your Web application. From the Configuration tab (see Figure E-14) you can set the following:

+   - The trust level of the application — Full trust enables all access (with the obvious exceptions regarding directly accessing the computer). Windows Azure partial trust works basically like Medium Trust in ASP.NET (see Chapter 34). However, it is even more restrictive, particularly around accessing environment variables or file IO.
+   - The number of instances your application will run — This can be changed later from the Windows Azure management screens.
+   - The "size" of the virtual machine that will run your application — These are basic combinations of number of CPUs, memory size, and disk space. While they will change as the underlying computers become more powerful, as of this writing the available sizes map to the following capacities:

![](bbox=[0.75, 0.55, 0.9, 0.75])

| VM SIZE | CPU CORES | MEMORY | DISK SPACE |
|---|---|---|---|
| Small | 1 | 1.7 GB | 250 GB |
| Medium | 2 | 3.5 GB | 500 GB |
| Large | 4 | 7 GB | 1 TB |
| ExtraLarge | 8 | 15 GB | 2 TB |