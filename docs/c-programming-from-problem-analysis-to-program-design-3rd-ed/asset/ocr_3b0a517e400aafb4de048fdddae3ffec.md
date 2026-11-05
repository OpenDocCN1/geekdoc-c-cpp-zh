When you select an **Access Database**, as shown in Figure 15-27, an instance of the AccessDataSource class is created. If you specify an ID for the data source, that name becomes the selector identifier that appears above the control on the form. Selecting **Database** creates an instance of SqlDataSource. If you select **Database**, the next dialog box enables you to create the Connection string. You could use this option with an Access database. However, if you select the **Access Database**, you do not have to set the Connection string property; you just identify the location of the Access .accdb file, as shown in Figure 15-28.

![](bbox=[0.175, 0.274, 0.853, 0.62])

**Figure 15-28** Relative address for the Access database

After you place your Access database in the **App_Data** directory, you browse to that location and a relative path is set, as shown in Figure 15-28.

You can place your database in the **App_Data** directory using the **Solution Explorer** window by right-clicking on the **App_Data** folder and selecting **Add Existing Item**. You can then **Browse** to its original location.

The database is now referenced by a relative path (for example, `~/App_Data/member.accdb`). You will see a new control for the **AccessDataSource** object on the page in **Design** mode, as shown in Figure 15-29.