# SQL Server Database Programming with C#

+   I. If users select the DataReader Method to perform this query, the ExecuteReader() method, which belongs to the initialized sqlCommand object in step C, is executed to perform this data query and return the queried result to the DataReader object.

+   J. By checking the HasRows property of the DataReader, we can confirm whether or not ExecuteReader() is running successfully. If that property returns a true, which means that at least one row has been matched and returned, a user-defined method FillFacultyReader() is called to get row and display each column on seven TextBoxes and a PictureBox in the Faculty Form window.

+   K. Otherwise, if the HasRows returns false, which means that the ExecuteReader() method fails a warning message is displayed to indicate that case.

+   L. A cleaning job is performed to clear the DataReader object since we no longer need it.

+   M. If any other query method is selected by the users, a warning message is displayed.

Now let's take care of the coding process for two user-defined methods, FillFacultyTable() and FacultyReader().

The first method is to collect all queried data columns from a filled DataTable, sqlDataTable, and display each of them on the relevant TextBox on the Faculty Form window. The retrieved faculty image should be displayed in a PictureBox object, PhotoBox, in the Faculty Form window.

Open the Code Window of the Faculty Form and enter the codes shown in Figure 5.77 into your window. Let's have a closer look at this picture of codes to see how it works.

+   A. The type of argument passed into this method is a reference, which is indicated by a keyword ref. This reference is similar to a fixed pointer in C++. When passing an argument in this way, it is equivalent to the address of that object into this method. Any modification to that is permanent and can be returned to the calling program.

+   B. Some local variables and objects are declared first, including a local integer index that works as a loop counter, and a TextBox array fBox[] that works as a data holder to store seven pieces of queried faculty information to be displayed in TextBoxes.

| RTOSSelect Project | FillFacultyTable(ref DataTable FacultyTable) |
|---|---|
| A | private void FillFacultyTable(ref DataTable FacultyTable) {
| B | int index = 0; TextBox[] fBox = { txtFacultyID, txtName, txtTitle, txtPhone, txtCollege, txtEmail };
| C | foreach (DataRow row in FacultyTable.Rows) {
| D | foreach (DataColumn column in FacultyTable.Columns) {
| E | if (index <= 6) {
fBox[index].Text = row[column].ToString();
index++;
} else {
| F | byte[] bimage = (byte[]])row["image"];
PhotoBox.Image = Image.FromStream(new MemoryStream(bimage));
}
}
}
 |

FIGURE 5.77 The codes for the user defined method FillFacultyTable().