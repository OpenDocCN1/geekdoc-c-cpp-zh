![](bbox=[0.374, 0.105, 0.642, 0.216])

Fig.VB-7.37

The **Add Connection** dialog box appears (Fig.VB-7.38).

+   20. *Select or enter* the name of the server to which you want to connect in the **Server name** combo box.
+   21. *Select* a radio button representing the authentication mode to log on to the server in the **Log on to the server** group (Fig.VB-7.38). In our case, we have selected the **Use SQL Server Authentication** radio button.

> > If you select the **Use Windows Authentication** radio button in the preceding step, skip the next two steps.

+   22. *Enter* the user name of your SQL Server account in the **User name** text box (Fig.VB-7.38).
+   23. *Enter* the password of your SQL Server account in the **Password** text box (Fig.VB-7.38).
+   24. *Select* the **Select or enter a database name** radio button in the **Connect to a database** group (Fig.VB-7.38).
+   25. *Select or enter* the name of the database from where you want to obtain data for your application, in the combo box under the **Select or enter a database name** radio button (Fig.VB-7.38). In our case, we have selected **Inventory** database.

> > You can click the **Test Connection** button to check whether or not a connection to the database server can be established with the settings that you have specified in the **Add Connection** dialog box.

+   26. *Click* the **OK** button to complete the steps to establish the connection with the selected database, as shown in Fig.VB-7.38:

![](bbox=[0.39, 0.546, 0.66, 0.734])

Fig.VB-7.38

A new data connection is created and added to the **Data Connections** node in **Server Explorer** (Fig.VB-7.39).