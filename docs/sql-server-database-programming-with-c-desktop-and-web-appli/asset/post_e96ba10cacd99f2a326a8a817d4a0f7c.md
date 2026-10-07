
value of that column must be converted to a string using the toString() method. If a typed DataSet is used, you can directly use the column name (no string to convert) to access that column without needing to use the toString() method. Each piece of information returned is assigned to the associated textbox, and will be displayed there. For the faculty image, a forced conversion is performed and a system method FromStream() is used to convert and display it in the Faculty Image box.

At this point we have finished all coding for this Windows-based Web service client project. We now start to run this client project to interface with our Web service, and furthermore to access and use the Web methods to perform our query.

Wait a moment! There is one issue you need to note before you can run this project, which is you must run our Web service WebWebServiceSelect first to allow our service available to all clients. Otherwise, you may encounter some exceptions (as the Web service or remote computer cannot be found) during your client project runs.

Open Visual Studio.NET and our Web service project WebWebServiceSelect, and click on the IIS Express to run it. One point is that our service project must be kept in the running status (even if has been minimized) in order to allow our client project to access and interface with it. An exception will be encountered if you stop our Web service when you try to access it from our client project.

Make sure that our Web service has been run once and it is in the running status, which can be identified by a small IIS icon on the task bar of your screen. You may need to click on the icon by right clicking on it and select Show All Applications item. The opened running status of this Web service project is shown in Figure 9.37.

Then start our client project by clicking the Start button from the project WinClientSelect Project. The running status is shown in Figure 9.38.

Select any query method and a faculty name, such as Jenny King, from the Faculty Name combo-box, and click the Select button to call the associated Web service method to retrieve the desired faculty record. The returned faculty record is displayed in the associated textboxes with the faculty photo, which is shown in 9.38.

You can select any other Web service method, either the Stored Procedure or the DataSet method, and other faculty members to perform this data query. The running result confirmed that

![](img/d59a47501d0a20fc0460a49c469c6fb7_578_0.png)

FIGURE 9.37 The running status of our web service WebWebServiceSelect project.

![](img/d59a47501d0a20fc0460a49c469c6fb7_579_0.png)

both our Web service and our Windows-based client projects are very successful. Click on the Back button to terminate our project.

A complete Windows-based client project **WinClientSelect Project** can be found from folder **ClassDB Projects/Chapter 9/WinClientSelect Solution** that is the Students folder on the CRC Press zip file (see Figure 1.2 in Chapter 1). You need to load both our client and our Web service projects from that state and install them in your computer if you want to run and test this client project. Also you must ensure our Web service project first to make sure that our Web service is ready to be consumed by that client project.

Next we develop a Web-based client project to consume a Web service by retrieving the desired information.

## 9.3.11 Build Web-Based Client Project to Consume the Web Service

Developing a Web-based client project to consume a Web service is very similar to developing a Windows-based client project to reference and accessing a Web service as we did in the last section. As long as a Web service is referenced by the Web-based client project, one can access and call any Method developed to perform the desired queries via the Web-based client project without any problem. Visual Studio will create the default document files, such as the Discovery Map file, the WSDL file and the DISCO file, for the client project no matter whether this Web service is consumed by a Windows-based or Web-based client.

To save time and space, we can modify an existing ASP.NET application **SQLServer Project** we developed in Chapter 8 to make it new Web-based client project **WebClientSelect Project**. In fact, we can copy and rename that project as our new Web-based client project. However, we prefer to create a new ASP.NET site application and copy and modify the Faculty page.

The developing process in this section can be divided into the following parts:

- 1) Create a new ASP.NET Web Application (.NET Framework) project and name it as **WebClientSelect Project** with **Web Forms** as Template.
- 2) Add an existing Web page Faculty.aspx WebSelectProject into our new project by selecting three files; Faculty.aspx, Faculty.aspx.cs and Faculty.aspx.designer.cs, and clicking on the Add button.

- 3) Add a Web service reference to our new project and modify the Web page window of the Faculty.aspx to meet our query requirements.

- 4) Modify the GUI and codes in the related methods of the Faculty.aspx.cs file to call the associated Web method to perform our query. These modifications include the following sections:

    - a. Modify the added Faculty_aspx by adding a label, Query Method, and a combobox, ComboMethod, to enable users to select different query method.
    - b. Modify the codes in the Page_Load() method of the Faculty.aspx.cs file.
    - c. Modify the codes inside the Select's click method.
    - d. Add three-user methods: ProcessObject(), FillSelectObject() and FillFindByDataSet(). These methods are basically identical with those developed in the last Windows-based client project WinClientSelectProject, and one can copy and paste them into our new project. The only modification is for the ProcessObject() method.
    - e. Modify the codes in the Back's click method.

Now start with the first step listed above.

### 9.3.11.1 Create a New Site Project and Add an Existing Web Page

Open Visual Studio.NET and go to the File | New Project to create a new ASP.NET Application project. Enter WebClientSelect Project and WebClientSelect Solution in the Project name and Solution name respectively, and C# in the Location box. Click on the Create button to select the Web Forms item, and click on the Create to create this Web application project.

Perform the following operations to add all existing Web pages related to Faculty.aspx into our new web project:

- 1) Right-click on our new project WebClientSelect Project from the Solution explorer window, and select the item Add | Existing Item from the popup menu.
- 2) Browse to our new project WebClientSelect Project from the Solution explorer window, and select the item Add | Existing Item from the popup menu.

- 3) Add a Web service reference to our new project and modify the Web page window of the Faculty.aspx to meet our query requirements.

- 4) Modify the GUI and codes in the related methods of the Faculty.aspx.cs file to call the associated Web method to perform our query. These modifications include the following sections:

    - a. Modify the added Faculty_aspx by adding a label, Query Method, and a combobox, ComboMethod, to enable users to select different query method.
    - b. Modify the codes in the Page_Load() method of the Faculty.aspx.cs file.
    - c. Modify the codes inside the Select's click method.
    - d. Add three-user methods: ProcessObject(), FillSelectObject() and FillFindByDataSet(). These methods are basically identical with those developed in the last Windows-based client project WinClientSelectProject, and one can copy and paste them into our new project. The only modification is for the ProcessObject() method.
    - e. Modify the codes in the Back's click method.

### 9.3.11.2 Add a Service Reference and Modify the Web Form

Open Visual Studio.NET and our Web service project WebWebServiceSelect, and click on the IIS Express to run it. One point is that our service project must be kept in the running status (even if has been minimized) in order to allow our client project to access and interface with it. An exception will be encountered if you stop our Web service when you try to access it from our client project.

Make sure that our Web service has been run once and it is in the running status, which can be identified by a small IIS icon on the task bar of your screen. You may need to click on the icon by right clicking on it and select Show All Applications item. The opened running status of this Web service project is shown in Figure 9.37.

Then start our client project by clicking the Start button from the project WinClientSelect Project. The running status is shown in Figure 9.38.

Select any query method and a faculty name, such as Jenny King, from the Faculty Name combo-box, and click on the Select button to call the associated Web service method to retrieve the desired faculty record. The returned faculty record is displayed in the associated textboxes with the faculty photo, which is shown in 9.38.

You can select any other Web service method, either the Stored Procedure or the DataSet method, and other faculty members to perform this data query. The running result confirmed that

![](img/d59a47501d0a20fc0460a49c469c6fb7_578_0.png)

FIGURE 9.37 The running status of our web service WebWebServiceSelect project.

![](img/d59a47501d0a20fc0460a49c469c6fb7_579_0.png)

both our Web service and our Windows-based client projects are very successful. Click on the Back button to terminate our project.

A complete Windows-based client project **WinClientSelect Project** can be found from folder **ClassDB Projects/Chapter 9/WinClientSelect Solution** that is the Students folder on the CRC Press zip file (see Figure 1.2 in Chapter 1). You need to load both our client and our Web service projects from that state and install them in your computer if you want to run and test this client project. Also you must ensure our Web service project first to make sure that our Web service is ready to be consumed by that client project.

Next we develop a Web-based client project to consume a Web service by retrieving the desired information.

## 9.3.11 Build Web-Based Client Project to Consume the Web Service

Developing a Web-based client project to consume a Web service is very similar to developing a Windows-based client project to reference and accessing a Web service as we did in the last section. As long as a Web service is referenced by the Web-based client project, one can access and call any Method developed to perform the desired queries via the Web-based client project without any problem. Visual Studio will create the default document files, such as the Discovery Map file, the WSDL file and the DISCO file, for the client project no matter whether this Web service is consumed by a Windows-based or Web-based client.

To save time and space, we can modify an existing ASP.NET application **SQLServer Project** we developed in Chapter 8 to make it new Web-based client project **WebClientSelect Project**. In fact, we can copy and rename that project as our new Web-based client project. However, we prefer to create a new ASP.NET site application and copy and modify the Faculty page.

The developing process in this section can be divided into the following parts:

- 1) Create a new ASP.NET Web Application (.NET Framework) project and name it as **WebClientSelect Project** with **Web Forms** as Template.
- 2) Add an existing Web page Faculty.aspx WebSelectProject into our new project by selecting three files; Faculty.aspx, Faculty.aspx.cs and Faculty.aspx.designer.cs, and clicking on the Add button.

- 3) Add a Web service reference to our new project and modify the Web page window of the Faculty.aspx to meet our query requirements.
- 4) Modify the GUI and codes in the related methods of the Faculty.aspx.cs file to call the associated Web method to perform our query. These modifications include the following sections:

    - a. Modify the added Faculty_aspx by adding a label, Query Method, and a combobox, ComboMethod, to enable users to select different query method.
    - b. Modify the codes in the Page_Load() method of the Faculty.aspx.cs file.
    - c. Modify the codes inside the Select's click method.
    - d. Add three-user methods: ProcessObject(), FillSelectObject() and FillFindByDataSet(). These methods are basically identical with those developed in the last Windows-based client project WinClientSelectProject, and one can copy and paste them into our new project. The only modification is for the ProcessObject() method.
    - e. Modify the codes in the Back's click method.

Now start with the first step listed above.

### 9.3.11.1 Create a New Site Project and Add an Existing Web Page

Open Visual Studio.NET and go to the File | New Project to create a new ASP.NET Application project. Enter WebClientSelect Project and WebClientSelect Solution in the Project name and Solution name respectively, and C# in the Location box. Click on the Create button to select the Web Forms item, and click on the Create to create this Web application project.

Perform the following operations to add all existing Web pages related to Faculty.aspx into our new web project:

- 1) Right-click on our new project WebClientSelect Project from the Solution explorer window, and select the item Add | Existing Item from the popup menu.
- 2) Browse to our new project WebClientSelect Project from the Solution explorer window, and select the item Add | Existing Item from the popup menu.

- 3) Add a Web service reference to our new project and modify the Web page window of the Faculty.aspx to meet our query requirements.
- 4) Modify the GUI and codes in the related methods of the Faculty.aspx.cs file to call the associated Web method to perform our query. These modifications include the following sections:

    - a. Modify the added Faculty_aspx by adding a label, Query Method, and a combobox, ComboMethod, to enable users to select different query method.
    - b. Modify the codes in the Page_Load() method of the Faculty.aspx.cs file.
    - c. Modify the codes inside the Select's click method.
    - d. Add three-user methods: ProcessObject(), FillSelectObject() and FillFindByDataSet(). These methods are basically identical with those developed in the last Windows-based client project WinClientSelectProject, and one can copy and paste them into our new project. The only modification is for the ProcessObject() method.
    - e. Modify the codes in the Back's click method.

### 9.3.11.2 Add a Service Reference and Modify the Web Form

Open Visual Studio.NET and our Web service project WebWebServiceSelect, and click on the IIS Express to run it. One point is that our service project must be kept in the running status (even if has been minimized) in order to allow our client project to access and interface with it. An exception will be encountered if you stop our Web service when you try to access it from our client project.

Make sure that our Web service has been run once and it is in the running status, which can be identified by a small IIS icon on the task bar of your screen. You may need to click on the icon by right clicking on it and select Show All Applications item. The opened running status of this Web service project is shown in Figure 9.37.

Then start our client project by clicking the Start button from the project WinClientSelect Project. The running status is shown in Figure 9.38.

Select any query method and a faculty name, such as Jenny King, from the Faculty Name combo-box, and click on the Select button to call the associated Web service method to retrieve the desired faculty record. The returned faculty record is displayed in the associated textboxes with the faculty photo, which is shown in 9.38.

You can select any other Web service method, either the Stored Procedure or the DataSet method, and other faculty members to perform this data query. The running result confirmed that

![](img/d59a47501d0a20fc0460a49c469c6fb7_578_0.png)

FIGURE 9.37 The running status of our web service WebWebServiceSelect project.

![](img/d59a47501d0a20fc0460a49c469c6fb7_579_0.png)

FIGURE 9.39 Add a web reference.
