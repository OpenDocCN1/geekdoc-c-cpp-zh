Because each synchronization scenario requires different decisions, SQL Server Compact supports three different technologies for defining the synchronization:

+   > **Remote Data Access (RDA)** — RDA is the simplest means of configuring synchronization between SQL Server Compact and one of its larger brethren. With RDA, you create a new virtual directory under IIS. The virtual directory includes the SQL Server CE Agent DLL. Client applications then initiate the synchronization. Data can be pulled or pushed out of a single table, and you can query for a subset of the data. While this method is tempting, Microsoft has announced that further support for this technology is unlikely; they won’t be adding any additional features to it. Instead, developers are encouraged to make use of Sync Services.

+   > **Merge replication** — This is the replication system built into SQL Server. It is a DBA-centric model, whereby the database administrator configures the data shared between the applications. The SQL Server Agent then schedules the synchronization between server and client(s). This form of synchronization is powerful, but it is also the most complex to configure. It requires permissions to create the publications and synchronization schedule on the server, as well as to create the subscriptions on the client. Creating merge replication publications is supported only on SQL Server Standard Edition and higher, so you can’t create a merge replication between SQL Server Express and SQL Server Compact.

+   > **Sync Framework** — The Sync Framework provides the simplicity of RDA with the robustness of merge replication. They make it incredibly easy to create an application that uses the SQL Server Compact database as a local cache. With a bit of additional code, you can also use it for bidirectional synchronization.

Here’s an example of using Sync Framework to create a one-way synchronization:

+   1. Create a new Windows Forms Application project (here it is called `LocalCache`).
+   2. Add a new Local Database Cache item to the project (see Figure 12-11). As this will be used to cache data from the pubs database, it is called `PubsCache`.
+   3. The Local Database Cache item enables you to easily configure the Sync Framework, as it starts the Data Synchronization Wizard. The first step of the wizard is to configure the two connection strings: for server and client. Create a new server connection string to the `pubs` database used in Chapter 10. Once this is done, the wizard will add a new SQL Server Compact database to the project and create the client connection (see Figure 12-12).

![](bbox=[0.46, 0.12, 0.88, 0.48])

# FIGURE 12-10