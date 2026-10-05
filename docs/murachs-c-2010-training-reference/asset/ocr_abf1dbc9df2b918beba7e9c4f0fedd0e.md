# Setup project that deploys an application with a database file

![](bbox=[0.095, 0.088, 0.875, 0.518])

# The connection string for the application

Data Source=\SqlExpress;AttachDbFilename=|DataDirectory|\Data\MMABooks.mdf;Integrated Security=True;User Instance=True

# Description

+   - To use a database that's available via a LAN, you set the connection string and provide users with permissions to the database as you do when use ClickOnce deployment.
- To deploy a database to the user's computer along with other files for an application, you use the File Editor to add the database file to the folder where you want the database stored on the user's computer.
- If you included the database file in the application you're deploying, the connection string is generated with a DataDirectory specification like the one you used in the last figure. For Setup deployment, this is the directory that contains the executable file for the application.
- If you want to store the database files in a directory other than the one that contains the executable file, you'll need to modify the connection string as shown above.
- To include SQL Server 2008 as a prerequisite, select the Setup project in the Solution Explorer and use the Project\Properties command to display the Properties dialog box. Then, click the Prerequisites button to display the Prerequisites dialog box shown in figure 25-4.

Figure 25-13 How to deploy a database application using a Setup program