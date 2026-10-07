# 436 SQL Server Database Programming with C#

Let's have a closer look at this piece of codes to see how it works.

+   A. A first counter `intIndex` is declared and it is used for the `for()` loop to pick up each column retrieved from the Faculty table in our sample database.
B. A textbox array `box[]` is generated to hold seven textboxes to be filled later via the `for()` loop with seven columns stored in the `DataReader`.
C. A `while()` loop is executed as long as the condition `Read()` method is `true`, which means that a valid record is read out from the DataReader. This method will return `false` if no valid record is read out from the DataReader, which in this application, this `while()` loop is executed one time since all data have been read only one row (one record) read out from the DataReader.
D. A `for()` loop is utilized to pick up each data column read out from the DataReader object, and assign each of them to the associated textbox control on the Faculty page via the textbox `box[]`. The `selectedIndex` is used to identify each column from the DataReader. The terminal column number is equal to `FieldCount – 2` since the last column (7) of the faculty table is a faculty image, `fimage`, which is an image object and cannot be counted as. The 7 columns the text information for a faculty record are arranged from column 0 to 6 (`FieldCount =`).
E. Since the image is stored in the last column with a format of binary data, therefore we need to get and convert it to a `byte[]`.
F. Because there is no `PictureBox` object available in a Web page, we need to convert that image from a `byte[]` array to a 64-bit String, and assign it to the `ImageUrl` property of the Image object in the Faculty page: `PhotoBack`.

Finally, let's take care of the coding for the `Back` button click method. The function of this piece of codes is to return the coding to the Selection page as this button is clicked. Double-click the `Back` button from the Design View of the Faculty page window to open this method and entering the coding into this method, which is shown in Figure 8.25.
This coding is straightforward and easily understood. The `Redirect()` method of the Response object is executed to direct the client from the current Faculty page back to the Selection page when this button is clicked by the user. The server returns the Selection page to the client when this button is clicked and a request is sent to the server.
Now we have finished all coding development for the Faculty page. It is the time for us to run the project to test out. Click the `IIS Express` to run our project. Enter the suitable username and password, such as `jerry`, to the Login page, select one faculty member, such as Yang Bai, and then click the Select button to retrieve the selected faculty information from the database. All information related to that selected faculty is retrieved and displayed in this Faculty page, as shown in Figure 8.26.
Click on the `Back` button to return to the Selection page, and then click the Exit button to terminate our project. So for our Web application is successful.

| SQLWebSelect Project | cmdBack_Click(object sender, EventArgs e) |
|---|---|
| protected void cmdBack_Click(object sender, EventArgs e) { 
  Response.Redirect("Selection.aspx");
 } |

FIGURE 8.25 The codes for the back button's click method.