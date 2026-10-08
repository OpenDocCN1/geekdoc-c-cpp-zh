# Chapter 22 Databases and LINQ

![](bbox=[0.239, 0.103, 0.759, 0.283])

Fig. 22.25 | Results of the Display Query Results app's Titles ending with "How to query.

# 22.6.1 Creating the Display Query Results GUI

Perform the following steps to build the Display Query Results app's GUI.

### Step 1: Creating the Project
Perform the steps in Section 22.5.2 to create a new Windows Forms Application project named DisplayQueryResult in the same solution as the DisplayTable. Rename Form1.cs source file to TitleQueries.cs. Set the Form's Text property to Display Query Results. Be sure to add references to BooksExample and EntityFramework libraries, add the connection string to the App.Config file and set the DisplayQuery-Result as the startup project.

### Step 2: Creating a DataGridView to Display the Titles Table
Follow Steps 1 and 2 in Section 22.5.3 to create the data source and the DataGridView. For this example, select the Title class (rather than Author) as the data source, and drag the Title node from the Data Sources window onto form. Remove the columns from DataGridView, as it will not be used in this example.

### Step 3: Adding a ComboBox to the Form
In Design view, add a ComboBox named below the DataGridView on the Form. Users will select the names of the query to execute from this. Set the ComboBox's Dock property to Bottom and the DataGridView's Dock property to Fill.
Next, add all the names of the queries to the ComboBox. Open the ComboBox String Collection Editor by clicking Edit Items... You can also access the String Collection Editor from the ComboBox's smart tag menu. A smart tag provides you with quick access to common properties you may set for a control (such as the Multiline property of a TextBox), so you can set these properties directly in Design view, rather than in the Properties window. You can open the control's smart tag menu by

appears in the control's upper-right corner in Design view when the control is selected. In the String Collection Editor, add the following three items to queryComboBox—one for each of the queries we'll create: