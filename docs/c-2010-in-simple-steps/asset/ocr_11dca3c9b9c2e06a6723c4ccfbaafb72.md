![](bbox=[0.26, 0.15, 0.76, 0.3])

Fig.C#-13.17 shows the Service.cs and app.config files that are generated after executing the svcutil.exe command.

# Note

The port number, which is 49544, may vary according to your system.

Now, let's perform the following steps to create a WCF client application:

+   1. Open Visual Studio 2010 and create a Windows Forms application, WCFClient.
+   2. Set the Text property of the form to WCF Client.
+   3. Right-click the name of the project in Solution Explorer and select the Add Service Reference option from the context menu to add the reference of the WCFServic e WCF Service after creating the WCFClient application.
+   4. Enter the address of the WCFServic e WCF Service and click the Go button in the Add Service Reference dialog box. The list of services is displayed (Fig.C#-13.18).
+   5. Click the OK button to add service reference, as shown in Fig.C#-13.18:

![](bbox=[0.26, 0.55, 0.76, 0.76])

6. Add three Label controls, two TextBox controls, and a Button control and set their Text properties, as shown in Fig.C#-13.19: