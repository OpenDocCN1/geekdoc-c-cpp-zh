# Data Binding with Silverlight Application

You can perform data binding in a Silverlight application also. A Silverlight application like an ASP.NET application can be displayed in the Web browser. Unlike Silverlight 1, Silverlight 2 has controls that support data-binding features. The data-binding capabilities of Silverlight offer more power and flexibility of data with less runtime code. For data binding in Silverlight, you can use the DataGrid control. Let’s create a Silverlight application to display data:

+   1. Create a Silverlight Application named DataBindinginSilverlightCS (available on the CD).
+   2. Click the OK button in the New Project dialog box. The New Silverlight Application dialog box opens (Figure 17.49).
+   3. Select the Host the Silverlight application in a new Web site check box for hosting the Silverlight content, in the New Silverlight Application dialog box.
+   4. Select Silverlight 3 in the drop-down list labeled Silverlight Version, and then click the OK button, as shown in Figure 17.49:

![](bbox=[0.205, 0.355, 0.75, 0.69])

Figure 17.49: Specifying a Host for a Silverlight Application

This creates two projects in your application named DataBindinginSilverlightCS and DataBindinginSilverlightCS.Web. The first project, DataBindinginSilverlightCS is the Silverlight application. The second project, DataBindinginSilverlightCS.Web is created for you as a test environment for the Silverlight project.

+   5. Create a connection to the Employees table in the Northwind database from the Server Explorer window. The Server Explorer window, if not already open, can be opened by selecting the View→Server Explorer menu bar option. After creating the connection, you need to create the Web service.
+   6. Right-click the test project, DataBindinginSilverlightCS.Web, and select the Add → New Item option for creating a WCF service, as shown in Figure 17.50: