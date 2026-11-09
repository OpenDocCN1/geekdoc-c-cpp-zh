Table 6.20 lists the noteworthy methods of the `DetailsView` class:

**Table 6.20: Noteworthy Methods of the DetailsView Class**

| Method | Description |
| --- | --- |
| ChangeMode | Enables you to switch the DetailsView control to the specified mode |
| DataBind | Enables you to bind data from the data source to the control |
| DeleteItem | Enables you to delete the current record from the data source |
| InsertItem | Enables you to insert the current record in the data source |
| IsBindableType | Specifies whether or not the specified data type can be bound to a field in the DetailsView control |
| UpdateItem | Updates the current record in the data source |

Now, let's create a Web application to learn how to use the `DetailsView` control that displays data from a database by performing the following steps:

+   1. Click *Start*→*All Programs*→*Microsoft Visual Studio 2010*→*Microsoft Visual Studio 2010*.
+   2. Select *File*→*New*→*Web Site* from the menu bar.
+       The New Web Site dialog box appears.
+   3. Select *Visual C#*→*ASP.NET Web Site* from the middle templates pane.
+   4. Set the name of the Web site as *DetailsviewControl*.
+   5. Click the *OK* button.
+       The *DetailsViewControl* application is created.
+   6. Drag and drop the *DetailsView* control on the *Default.aspx* page from the *Toolbox*.
+   7. Open the *DetailsView Tasks* menu using the smart tag and select the *New data source* option from the *Choose Data Source* drop-down list to create the connection with the database as done earlier.
+   8. Change the appearance of the *DetailsView* control using the *AutoFormat* dialog box.
+   9. Set the *Default.aspx* page as start page as done earlier.
+   10. Press the *F5* key to execute the application. The output of the application appears, as shown in Fig.ASP-6.37:

![](bbox=[0.33, 0.55, 0.7, 0.77])

Fig.ASP-6.37

After learning about the `DetailsView` control, let's learn about the `FormView` control.