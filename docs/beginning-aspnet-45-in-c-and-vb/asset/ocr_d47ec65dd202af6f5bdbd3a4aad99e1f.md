+   2. In the window that appears, expand SQL Server Network Configuration, locate your instance of SQL Server, and click it to display the list with available protocols. If you're running a 64-Bit version of Windows, you see an additional node with this name, followed by (32-Bit). In that case, find the one that contains the Protocols for SQLEXPRESS node. Figure B-1 shows the list for a SQL Server instance called SQLEXPRESS on a 32-Bit machine.
+   3. In the list with protocols on the right, right-click Named Pipes and choose Enable if its status is currently set to Disabled.
+   4. Repeat the previous step, but now enable TCP/IP.
+   5. Restart SQL Server. To do this, click SQL Server Services in the SQL Server Configuration Manager (shown in Figure B-1), then right-click your server and choose Restart. If you get an error about security permissions, you may need to reboot your computer instead.

![](bbox=[0.19, 0.3, 0.8, 0.52])

FIGURE B-1

SQL Server now allows incoming connections from remote machines. However, before you can actually use your databases, you need to attach them to SQL Server first. This is described in the following section.

> NOTE If you have trouble connecting to SQL Server, make sure that SQL Server is installed and running. To verify this, open the Control Panel and then open the Administrative Tools section found in the System and Security category. Next, open the Services item and then verify that the SQL Server instance you are connecting to is running. If you installed SQL Server Express on your local machine with the default instance name, the service is called SQL Server (SQLEXPRESS).

# Attaching Databases to SQL Server

SQL Server Express enables you to work with database files in two ways: you can either attach them at run time using a special attribute in the connection string, or you can attach them using tools such as Management Studio before you start using the database.