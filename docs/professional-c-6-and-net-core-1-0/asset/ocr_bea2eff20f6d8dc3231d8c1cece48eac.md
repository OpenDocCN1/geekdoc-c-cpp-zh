> **NOTE** *This chapter does not cover the `DataSet` to have tables in memory. Datasets enable you to retrieve records from a database and store the content within in-memory data tables with relations. Instead you should use Entity Framework, which is covered in Chapter 38, “Entity Framework Core.” Entity Framework enables you to have object relations instead of table-based relations.*

# Sample Database

The examples in this chapter use the AdventureWorks2014 database. You can download this database from https://msftdbprodsamples.codeplex.com/. With this link you can download a backup of the AdventureWorks2014 database in a zip file. Select the recommended download—Adventure Works 2014 Full Database Backup.zip. After unzipping the file, you can restore the database backup using SQL Server Management Studio as shown in Figure 37.1. In case you don’t have SQL Server Management Studio on your system, you can download a free version from http://www.microsoft.com/downloads.

![](bbox=[0.1, 0.43, 0.89, 0.83])

# Figure 37.1

The SQL server used with this chapter is SQL Server LocalDb. This is a database server that is installed as part of Visual Studio. You can use any other SQL Server edition as well; you just need to change the