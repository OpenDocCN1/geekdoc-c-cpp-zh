# Modifying Connection Strings

If you have a problem connecting to a database, it might be necessary to modify the connection string and reattach the database to your application. You can use several methods to change the connection string. You read earlier about changing the XML `app.config` file when the connection string is saved with the application. Another approach is to use the **Settings** page of the **Property Designer** to modify the project's settings. You access this page through the **Solution Explorer** window. The `Settings.settings` file is located inside the **Properties** folder. Double-clicking on the `Settings.settings` file opens the application's settings file. From there, you can click on the **Value** box and **Browse** to attach the database file. Figure 14-37 shows both the `Settings.settings` window and the `app.config` file. This might be necessary if you have a problem connecting to the database.

![](bbox=[0.174, 0.339, 0.912, 0.665])

Figure 14-37   Modifying the Settings.settings file

![](bbox=[0.176, 0.731, 0.238, 0.781])

You can copy SQL Server database files from the application’s solution folder to the directory that contains your other SQL Server databases. For example, my SQL Server database files are stored at `C:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data`. To find the path for your SQL Server database file, search for files ending in `.mdf`.

As stated previously, when you attach a database file to your application, you might receive a message asking whether you want a local copy of your database stored with the application. Having a local copy works fine if you only intend to display the data. It also makes testing easier. However, if you are making changes to the database and want the database changes to be available to other applications, you might not want to make a local copy of it.