# Access Data in ASP.NET

D. The Parameter object is initialized by assigning the dynamic parameter's name and value to it.

E. The ExecuteReader() method of the Command object is called to execute the query command to retrieve back selected faculty information, and assign it to the DataReader object.

F. By checking the HasRows property of the DataReader, we can determine whether this query is successful or not. If it is greater than zero, which means that at least one row is retrieved from the Faculty table in the database and therefore the query is successful, a user-defined method FillFaculty(), which we will build in the next part, is to fill text boxes on the Faculty page with the retrieved image.

G. Otherwise if the HasRows property is equal to zero, which means that no row has been retrieved from the database and the query is failed. A warning message is displayed in the client by calling the Write() method of the Response object.

H. All data components used for this query are released after the query.

At this point we have the first part-coding for the Select button's Click method. Now let's have the second part coding for this method.

# 8.4.8.3 Develop the Codes for Other Methods

Next let's take care of the coding for other methods in this Faculty page. This includes the coding for the following methods:

+   1) User-defined method FillFaculty().
2) Back button's Click method.

First let's take care of the user-defined method FillFaculty(). The function of this method is to fill text boxes with pieces of queried faculty information and display the queried faculty image in this page.

One significant difference in displaying an image between the Windows-based and the Web-based application is that the Image.Url property belongs to the control System.Ui.WebControls. Image, is utilized to access the matched faculty photo file and only the name of an image file is needed to display the associated image in the Web-based application. In the Windows-based application, a System.Drawing() must be used to display an image on the image file's name.

```
private void FillFacultyReader(SqlDataReader FacultyReader)
{
  int index;
  TextBox[] fbox = { txtFacultyID, txtName, txtOffice, txtPhone, txtCollege, txtEmail };
  while (FacultyReader.Read())
  {
    for (int index = 0; index < FacultyReader.FieldCount-2; index++)
    {
      fbox[index].Text = FacultyReader.GetString(index);
      byte[] image = (byte[])FacultyReader["Image"];
      string img = Convert.ToBase64String(image);
      Photos.ImageUrl = String.Format("data:image/jpeg;base64,{0}", img);
    }
  }
}
```

FIGURE 8.24 The coding for the user-defined method FillFacultyReader().