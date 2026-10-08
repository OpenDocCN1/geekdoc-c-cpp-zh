# Adding the Data Model and Registering the Data Context

Now, it is necessary to add the link to the data that the Dynamic Data framework must consider to generate the website. To do this, you must do the following:

+   - Create a data folder, or the classes that represent data entities.

+   - Register the aforementioned data context with Dynamic Data. By this way, the framework will be able to use it.

First, in this case, follow these steps to create a copy of the database file in the project. However, in other cases, you may wish to use other methods to link the database.

+   1. Right-click on the App_Data folder in the Solution Explorer and select Add Existing Item in the context menu appears. A file selection box will appear.

+   2. Select Data Files in the file type combo box. (It shows Web Files by default.)

+   3. Navigate to the folder that contains the SQL Server database (RetroGames.mdf), select it, and click Add. It will appear in the App_Data folder, as shown in Figure 17-3. Additionally, you will be able to access it through Data Connections in the Server Explorer.

![](bbox=[0.139, 0.452, 0.405, 0.739])

![](bbox=[0.473, 0.563, 0.659, 0.739])

FIGURE 17-3: Adding the SQL Server database file to the App_Data folder

FIGURE 17-2: Organization of files in folders

Now, follow these steps to create a data model using LINQ to SQL:

+   1. Right-click on the project's name (C:\...\RetroGamesWeb1\) in the Solution Explorer and select Add ASP.NET Folder -> App_Code folder in the context menu appears. The IDE will add your App_Code folder, as shown in Figure 17-4.

![](bbox=[0.733, 0.825, 0.939, 0.888])

FIGURE 17-4: App_Code folder added