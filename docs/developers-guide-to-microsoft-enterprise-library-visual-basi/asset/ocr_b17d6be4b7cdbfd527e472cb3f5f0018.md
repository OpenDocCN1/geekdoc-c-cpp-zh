# USING THE DATABASE BACKING STORE

You can easily and quickly configure the Caching block to use a database as your persistent backing store for cached data if you wish. Enterprise Library contains a script and a command file that you can run to create the database (located in the \\Blocks\\Caching\\Src\\Database\\Scripts folder of the Enterprise Library source code). We also include these scripts with the example for this chapter.

The scripts assume that you will use the locally installed SQL Server Express database, but you can edit the CreateCachingDb.cmd file to change the target to a different database server. The SQL script the command file executes creates a database named Caching, and adds the required tables and stored procedures to it.

However, if you only want to run the example application we provide for this chapter, you do not need to create a database. The project contains a preconfigured database file (located in the bin\\Debug folder) that is auto-attached to your local SQL Server Express instance. You can connect to this database using the Microsoft® Visual Studio® Server Explorer to see the contents, as shown in Figure 3.

![](bbox=[0.125, 0.362, 0.865, 0.642])

FIGURE 3 Viewing the contents of the cache in the database table

To configure caching to a database, you simply add the database cache storage provider to the cache manager using the configuration console, and specify the connection string and ADO.NET data provider type (the default is System.Data.SqlClient, though you can change this if you are using a different database system).

You can also specify a partition name for your cache, in the same way as you can for the isolated storage backing store provider. This allows you to separate the cached data for different applications (or different cache managers) for the same user by effectively segregating each one in a different partition within the database table.

Other than the configuration of the cache manager to use the database backing store, the code you use to cache and retrieve data is identical. The example, Cache data in a