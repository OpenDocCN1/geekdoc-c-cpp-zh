
# SQL Server Database Programming with C#

## Add Web Reference
Navigate to a web service URL and click Add Reference to add all the available services.

![](img/d59a47501d0a20fc0460a49c469c6fb7_572_0.png)

| WebSelect | Web services found at this URL: |
|---|---|
| 1 Service Found: | |
| - WebServiceSelect | |

Web reference name:
WS_SQL_Select
[Add Reference]

FIGURE 9.32 The add web reference wizard.

- 2) Then open another Visual Studio.NET 2022 in the Administrator mode and open our client project WinClientSelect Project.
- 3) Right click on our client project WinClientSelect Project from the Solution Explorer window, and select the item Add | Service Reference from the popup menu to open the Add Service Reference wizard.
- 4) Click on the Advanced button at the lower-left corner on that to open the Web Service Settings window.
- 5) Click on the Add Web Reference button in the lower-left corner to open the Web Reference wizard, which is shown in Figure 9.32.
- 6) Paste the code we copied from step 1 into the URL box in the Add Web Reference wizard and click on the Arrow button to enable the Studio.NET to search it.
- 7) When the web service is found, the name of our Web service is displayed in the right pane, which is shown in Figure 9.32.
- 8) Alternately you can change the name for this Web reference from localhost to any meaningful name such as WS_SQL_Select in our case. Click on the Add Reference button to add this web service to our new client project.
- 9) Click on the Close button from our Web service built-in Web interface to terminate our service project.

Immediately you can find that the Web service WS_SQL_Select, which is under the folder Web References, has been added to the Solution Explorer window in our client project. This reference is the so-called Web service proxy class.

Next's develop the graphic interface by adding useful controls to interface to our Web service and display the queried information.

# ASP.NET Web Services

### 9.3.10.2 Develop the Graphic User Interface for the Windows-Based Client Project

Perform the modifications to our new project:

- 1) Rename the Form Object from the default name Form1 to our desired name WinClient Form.cs.
- 2) Rename the Window Form object from the default name Form1 to our desired name FacultyForm by modifying the Name property of the window.
- 3) Rename the form title from the default name Form1 to CSE_DEPT Faculty Form by modifying the Text property of the form.

To save time and space, we can use the GUI located in the project RTOUpdateDelete Project developed in Chapter 7. Open from the folder ClassDBs Projects Chapter 7 that is under the Students follow the CRC site (refer to Figure 1.2 in Chapter 1). Then open the Faculty form and select all controls from that form by going to the menu Edit | Select All, and then Edit | Copy menu to copy all controls selected from this form window.

To return our new Windows-based web client project WinSelectProject, open our form window and paste those controls we copied from the Faculty form in the project RTOUpdateDelete Project.

The purpose of the combo Query Method is to select one of three query methods developed in our Web service project to get the desired faculty information:

- 1) Method 1: Use an object to return our queried information.
- 2) Method 2: Use a stored procedure to return our queried information.
- 3) Method 3: Use a DataSet to return our queried information.

The Faculty Name combo control is used to select the desired faculty member as the input parameter for the Web name. In this application, only the Select and Back buttons are used.

The function of this project is: when the project runs, as the desired method and the faculty name have been selected from the associated controls, the Select button will be clicked by the user. Our client project will connect to our Web service based on the Web reference provided, and the selected method will be called based on the method chosen from the Query method control, to retrieve the desired faculty record from our sample database, and display it in this graphic interface.

Now let's take at the code of processing for this project to connect to our Web service using the Web reference in the last section.

### 9.3.10.3 Develop the Code to Consume the Web Service

The coding job is divided into four parts:

- 1) The coding for the constructor of the FacultyForm to initialize the Query Method combo control and the Faculty Name combo control. The first initialization will setup three Web methods that can be selected by the user to perform the data query from the Web Service. The second one is to set a default list of faculty members that can be selected by the user to perform the associated faculty information query.
- 2) The coding for the Back button's Click method to terminate the project.
- 3) The coding for the Select button's Click method.
- 4) The coding for other user-defined methods, such as ShowFaculty(), ProcessObject(), FillFacultyObject() and FillFacultyDataSet().

The main coding is performed inside the Select button's Click method. As we discussed, this button is clicked by the user, a connection to our Web Service needs to be established using the Web reference we set up in the previous section. Therefore, we need first to create an object on Web Reference or instantiate that Web Service to get an instance, then we can access the different Web Methods to perform our data query via that instance. This process is called to instantiate the proxy class and invoke the Web Methods. The protocol to instantiate a proxy class is:

```
WebReference.WebServiceInstance = new WebReference.WebService();
```

After this miss instance, then a connection between our client project and our Web service can be setup by using this instance. The pseudo-codes for this method are below:

- A. A new Web Service instance wsSelect is created using the protocol given above.
- B. A new wsSQLResult is also created and can be used as a mapping of the real object developed in the Web Service. We can easily access the Web method to perform our data query and pick the result from returning object by assigning it to the mapping object.
- C. A new DataSet object is created and it is used to call the Web method that returns a DataSet.
- D. Based on the method selected by the user using the Query Method combobox control, different Web methods can be used to perform the data query.
- E. The returned data that are stored in the real object are assigned to our mapping object, and each piece of information can be retrieved from this object and displayed in our graphic user interface.
- F. If a DataSet method is used, the returned DataSet object is assigned to our mapping DataSet and the method fillFacultyDataSet() is called to fill the textboxes in the client form with the information picked up from the DataSet.

Now let's start our coding for the constructor of the Faculty Form.

#### 9.3.10.3.1 Develop the Codes for the Constructor of the FacultyForm Class
Now let's begin to develop codes for the constructor of the FacultyForm class to complete the initialization jobs in step 1 above.

- Open the constructor of the FacultyForm class and enter the following codes that are shown in Figure 9.33 into this method.

| WinClientSelectFacultyForm | FacultyForm() |
|---|---|
| public FacultyForm() { |
| InitializeComponent(); |
| ComboName.Items.Add("Ying Bar"); |
| ComboName.Items.Add("David Blair"); |
| ComboName.Items.Add("Black Anderson"); |
| ComboName.Items.Add("Steve Johnson"); |
| ComboName.Items.Add("Geneney King"); |
| ComboName.Items.Add("Alice Brown"); |
| ComboName.Items.Add("Debby Angles"); |
| ComboName.Items.Add("Jeff Henry"); |
| ComboName.SelectedIndex = 0; |
| ComboMethod.Items.Add("Object Method"); |
| ComboMethod.Items.Add("Stored Procedure Method"); |
| ComboMethod.Items.Add("DataSet Method"); |
| ComboMethod.SelectedIndex = 0; |
| } | |
| A | B |

FIGURE 9.33 The coding for the constructor of the FacultyForm class.
