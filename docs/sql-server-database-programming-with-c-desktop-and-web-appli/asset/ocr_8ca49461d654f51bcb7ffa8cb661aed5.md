# 580 SQL Database Programming with C#

Click on the Close button that is located at the upper-right corner of this Web interface to terminate our service. A complete Web service project WebServiceInsert can be found from a folder ClassDB Projects\Chapter 9\WebServiceInsert that is under the Students folder at the CRC Press filter (refer to Figure 1.2 in Chapter 1).

At this point, we have finished all code jobs in our Web project in the service side. Next we need to develop some professional Windows-based and Web-based application projects with beautiful graphic user interfaces to use or consume the Web service application developed in this Web service project WebInsertProject. Those Windows-based and Web-based applications can be developed as Web service clients.

# 9.4.3 Build Windows-Based Clients to Consume The Web Services

To use or consume a Web service, we first need to create a Web service proxy class in our Windows- or Web-based applications. Then we can create a new instance of the Web service proxy class and execute the desired Web service methods in that service class. The process of creating a Web service proxy class is equivalent to add a Web reference to our Windows-based or Web-based applications.

# 9.4.3.1 Create a Windows-Based Consumer and a Web Service Proxy Class

Basically, adding a Web reference to our Windows-based or Web-based applications is to execute a search. During this process, Visual Studio.NET 2022 will find to all Web services available to our applications.

Open Visual Studio.NET 2022 in the Administrator mode and create a new C# Windows Forms App (.NET Framework) and name it as WinClientInsertProject and save it to the folder C:\Chapter 9.3.11 to Let's add a Web reference to our new project.

Refer to Section 9.3.12 to start this Web reference process. Perform the following operations to finish this:

+   1) Open our Web service project WebInsertProject, and click on the IIS button to run it.
2) Copy the URL from the Address bar in our running Web service project.
3) Then open our Windows-based client WinClientInsertProject from the Solution Explorer window,
4) Right click on the client Add | Service Reference from the popup menu to open the Add Service Reference wizard.
5) Click on the Advanced button located at the lower-left corner on this window to open the Service Reference Settings wizard.
6) Click on the Add Reference button to open the Add Web Reference wizard, which is shown in Figure 9.69.
7) Paste that URL we copied from step 2 into the URL box in the Add Reference wizard and click on the Arrow button to begin the Visual Studio.NET to search for it.
8) When the Web service is found, the name of our service is displayed in the right pane, which is shown in Figure 9.69.
9) Alternatively you can change the name for this Web reference from localhost to any meaningful, such as WS_SQLInsert, in our class. Click on the Add Reference button to add Web service as a new client project.
10) Click on the Close button from our Web service built-in Web interface window to terminate our service project.

Immediately, you can find that the Web service WS_SQLInsert, which is under the folder Web References, has been added to the Solution Explorer window in our client project. This reference is the so-called Web service proxy class.

![](bbox=[0.104, 0.946, 0.895, 0.995])