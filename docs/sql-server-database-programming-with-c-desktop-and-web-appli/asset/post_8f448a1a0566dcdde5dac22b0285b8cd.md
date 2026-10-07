
# SQL Server Database Programming with C#

SqlCommand, in which the query string and the connection object work together two arguments to simplify this assignment. Then the ExecuteReader() method of the SqlCommand object is called to run query. The query result is returned and assigned to the SqlDataReader object reader.

- C. Before the Faculty Name combo box is filled with all updated faculty names, it must be cleaned up and this step is necessary, otherwise all previous faculty names will be added together with this new addition.
- D. A while loop with the Read() method is used to check and pick each retrieved data from the first column (column 0) in the Faculty table since only one data column (faculty name) is retrieved. Then each row is assigned or added to the Faculty Name combobox. A sync method GetString(0) is used to convert the retrieved row from an object to a string value.
- E. Finally two objects used, reader and sCommand, are released.

Next let's build the CODES for the Insert Button event method.

## 8.5.3 Develop the Codes for the Insert Button Click Method

Open the Insert's Click method by double-clicking the Insert from the Design View of the Faculty page, and enter the codes that are shown in Figure 8.38 into this method. Let's have a closer look at this pieces of code to see how it works.

- A. The insert query string is declared and it contains eight pieces of information that is related to eight columns in the Faculty table in the database.
- B. The data components and local variables in the method are declared here. The SqlCommand object, sqlCommand, and a local integer variable, intInsert, are used to execute the data insertion action and held the result from the execution of the code.

| SQLWebInsert Project | cmdInsert_Click(object sender, EventArgs args) |
| :--- | :--- |

```c
protected void cmdInsert_Click(object sender, EventArgs args)
{
    string cmdString = "INSERT INTO Faculty (faculty_id, faculty_name, title, office, college, email, image)" +
                      "VALUES (@faculty_id, @faculty_name, @title, @office, @phone, @college, @image)";
    SqlCommand sqlCommand = new SqlCommand(cmdString);
    int intInsert;
    if (FileUpload.HasFile)
{
        Response.Write("<alert>Select an insert file using FileUpload!</script>");
    }
    else
{
        SqlCommand.Connection = new SqlConnection("SqlConnection");
        SqlCommand.CommandType = CommandType.Text;
        SqlCommand.CommandText = cmdString;
        InsertParameters.Add(sqlCommand);
        intInsert = sqlCommand.ExecuteNonQuery();
        SqlCommand.Dispose();
        if (intInsert == 0)
        {
            Response.Write("<alert>The data insertion is failed!</script>");
        }
        cmdInsert.Enabled = false;
    }
}
```

![](img/d59a47501d0a20fc0460a49c469c6fb7_476_0.png)

# Accessing Data in ASP.NET

- C. A FileUpload object, which is used to allow users to select and get a faculty image to be inserted in our database. If the user entered seven pieces of information into seven textboxes to be inserted, a new faculty record to formed, but forget to select a faculty image, checking the HasFile property of FileUploadImage can determine whether or not a valid faculty image has been selected. If that property is false, a warning message is displayed to users to do that image selection.
- D. Otherwise, if the property HasFile returns a True, which means that a valid faculty image has been selected, then the SqlCommand object can be initialized to perform this data insertion action.
- E. A user-defined method, InsertParameters(), will be built later, is executed to assign all input parameters to the Parameters of the command object.
- F. The ExecuteNonQuery() method of the command object is called to run the insert query to perform this data insertion action.
- G. A cleaning job is performed to release all objects used in the method.
- H. The ExecuteNonQuery() method will return a value to indicate whether or not this data insertion was successful. The value of this return data equals the number of rows that have been successfully inserted into the Faculty table. If a zero is returned, which means no row has been inserted into the database, a warning message is displayed using this method. Otherwise, the data insertion is successful.
- I. Another user-defined method, CurrentFaculty(), is executed to get the current or updated members from our database after this data insertion action is done, and display updated faculty names to the Faculty Name combo.
- J. The Insert button is disabled after the record is inserted into the database. To avoid the multiple insertions of the same record into the database, the Insert button will be enabled again when the content of the Faculty ID textbox is changed, which means that a new faculty record will be inserted.

Next lets take care of the coding development for all other methods, including all related user-defined methods that will be used for this data insertion action.

## 8.5.4 DEVELOP THE CODES FOR OTHER METHODS

The coding for other methods includes the following:

- 1. The System TextChanged event for the faculty_id textbox.
- 2. The user-defined method InsertParameters().
- 3. The user-defined method getFacultyImage().

As mentioned, after a new faculty record is successfully inserted into the Faculty table in our sample database, the Insert button should be disabled to avoid duplicate insertion to be occurred. However, this button should be enabled again when another faculty record is ready to be inserted. By checking the content of the faculty_id textbox, we can identify whether or not a new faculty record is ready to be inserted. If that content is changed, which means that a new faculty_id is entered, the TextChanged event of that textbox is triggered, and on this event, we will enable the button.

To do that, double-click on the faculty_id textbox from the Design View of the Faculty page to open its TextChanged event method, and enter the coding line:

```c
cmdInsert.Enabled = true ;
```

The detailed codes for the user-defined method InsertParameters() are shown in Figure 8.39.

# SQL Server Database Programming with C#

| SQLWebInsertProject | InsertParameters(SqlCommand cmd) |
| :--- | :--- |
private void InsertParameters(SqlCommand cmd) {
  byte[] bimage;
  bimage = getFaceImage();
  cmd.Parameters.Add("@id", SqlDbType.Char).Value = tfaceID.Text;
  cmd.Parameters.Add("@name", SqlDbType.Char).Value = tname.Text;
  cmd.Parameters.Add("@title", SqlDbType.Char).Value = ttitle.Text;
  cmd.Parameters.Add("@office", SqlDbType.Char).Value = tooffice.Text;
  cmd.Parameters.Add("@phone", SqlDbType.Char).Value = tphone.Text;
  cmd.Parameters.Add("@college", SqlDbType.Char).Value = tcollege.Text;
  cmd.Parameters.Add("@email", SqlDbType.Char).Value = temail.Text;
  cmd.Parameters.Add("@image", SqlDbType.Binary).Value = bimage;
}
```

**FIGURE 8.39** the codes for method InsertParameters().

**FIGURE 8.40** Detailed codes for the user defined method getFaceImage().

This coding is straightforward and easy to understand. By the first byte[] array, image is generated and another user-defined method, **getFaceImage()**, is called to get the selected face image. Each piece of new information is assigned to the input parameter by using the **Add()** method of the Parameters class of the Command object.
The detailed codes for the user-defined method **getFaceImage()** are shown in Figure 8.40. Let’s have a closer look at this piece of codes to see how it works.

- * A. A new namespace **System.IO** should be added first since we need to use some components under that namespace, as **Directory** and **Path**, in this method.
- * B. A local variable **length** is declared and this variable works as a holder to hold the length of the byte[] **FaceImage**, which will be used to store the selected face image, and declared and it will be used under the current project folder. — indicates that this is the current folder **SQLWebInsert Project**. The method MapPath() is used to set up this path or folder and assign it to the local string variable imgPath.
- D. First we need to check if this default folder is already exists in the machine by using the system method **Exists()**. If not, another system method, **CreateDirectory()**, is used to create it in our machine.
