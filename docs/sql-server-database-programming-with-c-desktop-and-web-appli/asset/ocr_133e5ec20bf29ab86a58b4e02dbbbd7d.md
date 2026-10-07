# ASP.NET Web Services

You can try to select different query methods with different faculty members to test this project. Our Web-based client project is very successful. Click on the Back button to terminate our client project.

A complete Web-based service client project WebClientSelect Project can be found in our folder Class\Chapter 9 that is under the Students folder at the C Prep ftp site (refer to Figure 1.2 in Chapter 1).

# 9.3.12 DEPLOY THE COMPLETE WEB SERVICE TO PRODUCTION SERVERS

When we finished developing and testing our Web service in our local machine, we need to deploy it to the .NET SDK or IIS 5 or higher virtual directory to allow users to access and use it via a production server. We may discuss this topic in the early section when we finished developing our Web project. The reason we delay this discussion until this section is that we do not have to perform this service deployment if we run Web service and accessing using a client project in our local computer (development server). However, we must deploy our Web service to IIS if we want to run it in a Web server (production server).

Basically, we have two ways to do this deployment; one is simply to copy our Web service to a server running the IIS 5 or higher, or to the folder that contains our virtual directory. Another way is to use the Builder by Visual Studio.NET to compile the Web project and the compiled files. The so-called virtual directory is a default directory that can be recognized and accessed by a Web server as IIS to run our Web services. In ways, we need a virtual directory to store our Web service files and allow Web server to pick up and run our Web service from our virtual directory. Now let's see how to create an IIS virtual directory.

The following steps describe how to add a Web service and create an IIS virtual directory using the Internet Information Services (IIS) Manager:

+   1) Create a folder to save your virtual directories. The folder under the Web service root folder C:\inetpub\wwwroot. In our case, create a new folder named Select and place it under the root folder C:\inetpub\wwwroot.
2) Open the Control Panel and select the item System and Security, then click on the Administrative Tools icon. On the opened list, double click on the item Computer Manager, then expand the item Services and Applications from the left pane and click the item Internet Information Services (IIS) Manager. Click the Current View tab on the bottom of this wizard. Two items are listed under this item: Application Pools and Sites.
3) Right-click on the item Sites and Add Website item, we use the Site name as for this site, and click on the expansion on the right of the physical path to the location of our Web service project location. In this case, it is C:\SQL DB Programming\Students\Class DB Projects\Chapter 9\WebService Selection\WebServiceSelect Project. Click on the OK button. However, it should be C:\Chapter 9\WebServiceSelection\WebServiceProject.
5) In our case, enter the server name DESKTOP-24JPUB in the Host name. However, you need to enter your server name into this. Then click on the Test Settings to test the Pass-through authentication of this service.
6) Click on the Close and the OK button to complete this adding operation.

After our service is added to the IIS, we can deploy our Web service by either copying files to this virtual directory or performing a pre-compile process. Starting from Visual Studio.NET 2017, Microsoft provides an easy way to help users to build, configure, perform settings and deploy the Web service on the IIS with a Publish tool.

![](bbox=[0.005, 0.946, 0.994, 0.996])