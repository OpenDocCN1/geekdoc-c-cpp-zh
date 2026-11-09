Table 6.22: Noteworthy Properties of the FormView Class

| Property | Description |
| --- | --- |
| HeaderText | Obtains or sets the text to display in the header row of a FormView control. |
| HorizontalAlign | Obtains or sets the horizontal alignment of a FormView control on the page. |
| InsertItemTemplate | Obtains or sets the custom content for an item in insert mode. |
| InsertRowStyle | Obtains a reference that allows you to set the appearance of the data row in a FormView control when the control is in insert mode. |
| ItemTemplate | Obtains or sets the custom content for the data row in a FormView control when the control is in read-only mode. |
| PageCount | Obtains the total number of pages required to display every record in the data source. |
| PageIndex | Obtains or sets the index of the displayed page. |

Table 6.23: Noteworthy Methods of the FormView Class

| Method | Description |
| --- | --- |
| ChangeMode | Enables you to switch the DetailsView control to the specified mode |
| DataBind | Enables you to bind data from the data source to the control |
| DeleteItem | Enables you to delete the current record from the data source |
| InsertItem | Enables you to insert the current record in the data source |
| IsBindableType | Enables you to determine whether the specified data type can be bound to a field in the DetailsView control |
| UpdateItem | Enables you to update the current record in the data source |

Let’s learn to use a FormView control in a Web application by performing the following steps:

+   1. Click Start→All Programs→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010.
+   2. Select File→New→Web Site from the menu bar.
+      The New Web Site dialog box appears.
+   3. Select Visual C#→ASP.NET Web Site from the middle templates pane.
+   4. Set the name of the Web site as FormViewControl.
+   5. Click the OK button.
+      The FormViewControl application is created.
+   6. Drag and drop the FormView control on the Default.aspx page from the Toolbox.
+   7. Click the smart tag of the FormView control and create the connection with the database as done earlier.
+   8. Change the appearance of the FormView control by using the AutoFormat dialog box as done earlier.
+   9. Set the Default.aspx page as the start page as done earlier.
+   10. Press the F5 key to execute the application. The output of the application appears, as shown in Fig.ASP-6.38: