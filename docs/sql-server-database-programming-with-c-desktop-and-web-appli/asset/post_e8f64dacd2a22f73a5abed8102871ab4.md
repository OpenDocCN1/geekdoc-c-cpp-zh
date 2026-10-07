
# 392
SQL Server Database Programming with C#

table, and then you can recover all related records in all child tables. The reason for this is that the Course is a parent table with the course_id as a primary key, and you cannot recover any other record without first recovering the deleted record from the parent table.

Click on the File | Save All menu item when you finished these recoveries to save those recovered records.

A complete RTOUpdateDelete Project that contains the updating and deleting function for the Course table can be found from a folder DB Projects\Chapter 7\RTOUpdateDeleteSolution from the Students folder at the CRC Press site (refer to Figure 1.2 in Chapter 1).

## 7.5 UPDATE AND DELETE DATA FROM THE DATABASE USING STORED PROCEDURES

As mentioned in the previous sections, performing the data updating among related tables is a very challenging. The good news is that most of the time it is unnecessary to update the primary key, or the faculty_id, in the Faculty table if we want to update any other information from the Faculty table into the database. Basically, it is better to insert a new record with a new faculty_id into Faculty than to update record, including the primary key faculty_id, because the primary key faculty_id is good for the lifetime of the database in actual applications. Based on the analysis above, we will perform the data updating for all columns in the Faculty table except the faculty_id in this section.

To delete records from related tables, we need to perform two steps: First we need to delete records from the child tables, and then we can delete a record from the parent table. For example, if we want to delete a record from the Faculty table, first we need to delete those records that are related to the record to be deleted from the Faculty table through the Login and the Course tables (child tables), and then we can delete the record from the Faculty table (parent table).

To save space, and we can modify an existing project to make it our new project.

### 7.5.1 UPDATE AND DELETE DATA AGAINST SQL SERVER DATABASE USING STORED PROCEDURES

To update and delete data using the stored procedures developed in the SQL Server database is very similar to the data updating and deleting we performed in the last section. With a small modification to the existing project RTOUpdateDelete Project, we can easily create our new project SPupdatedeleteProject to perform the data updating and deleting by calling stored procedures in the SQL Server database.

To develop our new project in this, we divide it into three sections:

- 1) Modify the existing project RTOUpdateDelete Project to create our new project SPupdatedelete Project.
- 2) Develop the data updating and deleting stored procedures in the SQL Server database.
- 3) Call stored procedures to perform the data updating and deleting functions for the faculty information using the Faculty form window.

Now let's start with the first step.

### 7.5.1.1 Modify an Existing Project to Create Our New Project

Open the Windows Explorer and create a new folder as C:\Chapter 7 in your local machine if you have not, and then browse to the folder Students\Class DB Projects\Chapter 7 that is located on the CRC Press ftp site (refer to Figure 1.2 in Chapter 1). Copy the entire solution folder RTOupdateDelete Data Updating and Deleting with Visual C#. Solution and paste it to our new folder C\Chapter 7. Perform the following operations to make it as our project:

- 1) Change the name of the Solution and the project from RTOUpdateDeleteSolution to SPUpdateDeleteSolution, from RTOUpdateDeleteProject.csproj to SPUpdateDeleteProject.csproj.
- 2) Also change the RTOUpdateDeleteProject.csproj to SPUpdateDeleteProject.csproj. Then double click on the project Project |SPUpdateDeleteProject.csproj to open this.
- 3) Go to the menu Item |SPUpdateDeleteProject Properties to change the project's window. Change the Assembly name and the Default name to SPUpdateDeleteProject and SPUpdateDeleteProject, respectively.
- 4) Click on the Assembly Information button to update the Assembly Information wizard, change the Title and the Product to SPUpdateDeleteProject. Click on OK button to close this.
- 5) Change the project name for all Form windows, including Login.cs, Faculty, Course.cs, Selection.cs and Student.cs, and as related class Designer.cs, from RTO UpdateDelete_Project to SPUpdateDelete_Project using the Rename dialog box.
- 6) Double click on the CProgram.cs from the Solution Explorer to open it, and change the namespace to SPUpdateDelete_Project.

Go to the File | Save All to save those modifications. Click on the Save, the Overwrite and the Save button again to save this project. Now we are ready to modify the codes in our new project to perform data updating and deleting actions by calling the stored procedures. The code modifications include the following parts:

- 1) Replace the query string in the Update button's Click method in the Faculty Form with the name of the data updating stored procedure that will be developed in the next section to allow the method to call the related stored procedure to perform the data updateing action.
- 2) Replace the query string in the Delete button's Click method in the Faculty Form with the name of the data deleting stored procedure that will be developed in the next section to allow the method to call the related stored procedure to perform the data deleting action.

Regularly, these two modifications should be performed after the stored procedures have been created in the SQL database since we know some information from the created stored procedures, such as the name of the stored procedure and the name of the input parameters, to execute these modifications to the stored procedures. By the similarity between this project and the last one, we assumed that we have known these pieces of information and we can put these pieces of information into these methods in advance. The assumed information includes:

- 1) The name of the data updating stored procedure is dbo.UpdateFacultySP.
- 2) The name of the input parameters are identical with those names for the user method UpdateParameters().
- 3) The name of the input dynamic parameter is @FacultyID.
- 4) The name of the data deleting stored procedure is dbo.DeleteFacultySP.
- 5) The name of the input dynamic parameter is @fname.

Based on those assumptions, we can need to modify our coding in the Update button's Click method. The key point is to remember the names of those input parameters and the name of the stored procedure, and put them into our stored procedure later when we developed it in the next section.

# SPUdateDelete Project

# SQL Server Database Programming with C#

| | cmddUpdate_Click(object sender, EventArgs e) |
|---|---|

```c
private void cmddUpdate_Click(object sender, EventArgs e)
{
    string cmdString = "dbo.UpdateFactory";
    SqlCommand sqlCommand = new SqlCommand();
    int inUpdate = 0;
    sqlCommand.Connection = loginForm.sqlConnection;
    sqlCommand.CommandType = CommandType.StoredProcedure;
    sqlCommand.CommandText = cmdString;
    sqlCommand.Parameters.Add(sqlCommand);
    inUpdate = sqlCommand.ExecuteNonQuery();
    sqlCommand.Dispose();
    if(inUpdate == 0)
        MessageBox.Show("The data update is failed!");
}
```

**FIGURE 7.30** The modified codes for the button click method.

Open the Update's Click method and modify its coding. Your finished modifications to this method are shown in Figure 7.30. The modified parts have been highlighted with the bold words. Let's see how this piece of modified codes works.

- **A.** The content of the query string should be equal to the name of the stored procedure, dbo.UpdateFactory.
- **B.** The CommandType of the Command object should be StoredProcedure to tell the project that a stored procedure should be called to perform the data updating as the project runs.

There is no modification to the user-defined method UpdateParameters(). But in order to clarify the correctness of those input parameters for the stored procedure to be built in the next section, the codes for that are shown here in Figure 7.31.
Try to remember these parameters since we need to use them when we build our stored procedure dbo.UpdateFactory().
Next let us modify the codes in the Delete's button click method. This open method performs two modifications to this method. Your finished method should show what is shown in Figure 7.32.

# SPUdateDelete Project

# UpdateParameters(ref SqlCommand cmd)

```csharp
private void UpdateParameters(ref SqlCommand cmd)
{
    byte[] image;
    image = getFaceImage();
    cmd.Parameters.Add("@name", SqlDbType.Char).Value = txtName.Text;
    cmd.Parameters.Add("@title", SqlDbType.Char).Value = txtTitle.Text;
    cmd.Parameters.Add("@office", SqlDbType.Char).Value = txtOffice.Text;
    cmd.Parameters.Add("@phone", SqlDbType.Char).Value = txtPhone.Text;
    cmd.Parameters.Add("@college", SqlDbType.Char).Value = txtCollege.Text;
    cmd.Parameters.Add("@email", SqlDbType.Char).Value = txtEmail.Text;
    cmd.Parameters.Add("@image", SqlDbType.Binary).Value = image;
    cmd.Parameters.Add("@fid", SqlDbType.Char).Value = txtIDField.Text;
}
```

**FIGURE 7.31** The codes for the user-defined method UpdateParameters().
