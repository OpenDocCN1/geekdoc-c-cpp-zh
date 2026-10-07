
# SQL Server Database Programming with C#

object. You can insert data into any data table by calling the ExecuteNonQuery() method that belongs to the Command class. We will concentrate on this method in part.

In this section, we provide a sample method RTOInsertProject to illustrate how to insert records into a SQL Server database using the runtime object method.

Now let's start to build the sample method RTOInsertProject to insert data into the SQL Server database using the runtime method. Recall in Sections 5.15.5, 5.15.6 and 5.16.3 in Chapter 5, we will discuss how to select data for the Faculty, Course and Form windows using the runtime object method. For the Faculty Form, a regular runtime selecting query is performed, and for the Student, the stored procedures are used to perform the runtime query.

We will concentrate on inserting data into the Faculty table from the Faculty Form window in this part.

In order to avoid duplication in the coding process, we will modify an existing project RTOSelect Project we developed in Chapter 5 to create our new RTOInsert Project used in this section.

## 6.5 INSERT DATA INTO THE SQL DATABASE USING THE RUNTIME OBJECT METHOD

Open the Windows Explorer and create a folder G\Chapter 6 if you have not yet done so. Then browse the folder DB Projects\Chapter 5\RTOSelect Solution that is located under the Students folder at the CRC press site, and copy the entire solution RTOSelect Solution to our new G\Chapter 6. Perform the following operational steps to make copied solution as our new solution and project:

- 1) Name the changes of the project from RTOSelect Solution to RTOInsert Solution, and RTOSelect Project to RTOInsert Project.
- 2) Change the project file name from RTOSelect Project.csproj to RTOInsert Project.csproj. Double-click on the RTOInsert Project.csproj to open this project.

- 1) Go to | RTOInsert Project Properties menu to open the project's property window. Change the Assembly name from RTOSelect Project to RTOInsert Project and the Default namespaces from RTOSelect_Project to RTOInsert_Project, respectively.
- 2) Click on the Assembly button to open the Assembly Information wizard, change the Title and Product to RTOInsert Project. Click on the OK to close this window.
- 3) Change the Startup object from RTOSelect_Project to (Not).
- 4) Go to the File | Save All menu to save those modifications. Click the Save button on the opened File explorer and Overwrite and save this project.
- 5) Right-click on the Login.cs folder in the Solution explorer and select the View Code item to open the solution and verify the Login.cs class file.
- 6) Change its namespace from the original RTOSelect_Project to our new namespace, RTOInsert_Project.
- 7) Open the Login.designer.cs by double-clicking it from the Solution Explorer window (you need to expand the Login.cs to find this file).
- 8) Change the top line from the original namespace RTOSelect_Project to our current namespace, Selection.cs and Student.cs, to change the namespaces for all of those files.
- 9) Repeat steps 5–7 for all other files, such as Faculty.cs, Course.cs, Selection.cs

## Data Inserting with Visual C#.NET

- 10) Open the main file, C# Program.cs, from the Solution Explorer window by double-clicking on that, and change its name to RTOInsert_Project.

Go to the File | Save menu item to save those modifications. Now you can build the project to confirm those modifications by going to the menu Item | Build Solution. A ‘successful’ message will be displayed in the Output window.

Now we are ready to develop the new project to perform data insertions. The coding process for this data insertion is divided into three steps:

- 1) The data validation after the data insertion.
- 2) The data validation after the data insertion.
- 3) The data insertion using the run time object.

The purpose of the first step is to confirm that all inserted data stored in each associated TextBox should be complete and valid. In other words, all TextBox should be non-empty. The second step is used to confirm that the data insertion is successful, in other words, the new inserted data should be in the desired table in the database and can be read and displayed in the Result Form.

> Unlike the returned-data query as SELECT, in a system query Full() is used to try to open a new database connection if any valid connection is existed between the database and the application, all non-returned data queries as INSERT, UPDATE and DELETE do not have this functionality to open a new connection between the database and the application if any valid connection is existed. Therefore the user must develop code to provide this kind of functionality to use non-returned data queries.

In this section, we want to use the Faculty Form to perform data insertion to the Faculty table in our sample database. Let’s start from the first step.

### 6.5.1 THE CODING PROCESS FOR THE DATA VALIDATION BEFORE THE DATA INSERTION

This validation can be considered as a pre-validation and can be performed by calling two user-defined methods. The first method is InitializeFacultyInfo() and it is used to set up a relationship between each item in the string FacultyInfo[] and each TextBox stored the faculty information. The second method is CheckFacultyInfo() and it is used to scan and check each TextBox to make sure no one of them is empty.

Open the code window to try to copy and enter the codes that are shown in Figure 6.30 to create two user-defined methods, InitializeInfo() and CheckFacultyInfo().

- A. A class-level string, FacultyInfo[], is added to this class, this is added to this class.
- B. Inside the user-defined method, InitializeInfo(). All TextBoxes stored a new record are assigned to this.
- C. Inside the user-defined method, CheckFacultyInfo(). A message will be displayed if this situation happened

[content]

# SQL Server Database Programming with C#

# RTOInsert Project

| | FacultyInfo() |
|---|---|
```csharp
public partial class FacultyForm : Form
{
  LogInfo loginForm = new LogInfo();
  string[] FacultyInfo = new string[7];
}

private void InitializeInfo()
{
  FacultyInfo[0] = txtFacultyID.Text;
  FacultyInfo[1] = txtFacultyName.Text;
  FacultyInfo[2] = txtOffice.Text;
  FacultyInfo[3] = txtPhone.Text;
  FacultyInfo[4] = txtCollege.Text;
  FacultyInfo[5] = txtEmail.Text;
  FacultyInfo[6] = txtEmail.Text;
}

private int CheckFacultyInfo()
{
  int pos = 0; check = 0;
  for (pos = 0; pos <= 6; pos++)
  {
    if (FacultyInfo[pos] == string.Empty)
      check++;
  }
  return check;
}
```

FIGURE 6.30 The codes for the data validation process after a new record has been inserted

### 6.5.2 The Coding PROCESS FOR THE DATA VALIDATION AFTER THE DATA INSERTION

After a new record has been inserted into the Faculty table in our sample database, we need to check and confirm whether data insertion is successful or not. Fortunately, we do not need to create any new method to do that confirmation; we can use the Select button with our Click method to do checking. But we need to update all faculty names stored in the Faculty Name combobox, ComboName, to enable users to select the desired or the newly inserted faculty member to do that checking. Thus, we need to build a new method CurrentFaculty() in our project to do that job.

```csharp
private void CurrentFaculty()
{
  SqlDataReader sqlReader;
  SqlConnection com = loginForm.sqlConnection;
  SqlCommand sqlCommand = new SqlCommand("SELECT * FROM Faculty", com);
  sqlReader = sqlCommand.ExecuteReader();
  while (sqlReader.Read())
  {
    ComboName.Items.Add(sqlReader["FacultyName"].ToString());
  }
}
```
