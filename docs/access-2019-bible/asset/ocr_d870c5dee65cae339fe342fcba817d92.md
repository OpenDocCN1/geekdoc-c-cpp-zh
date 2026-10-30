**Exporting:** Exporting copies data from an Access table into a text file, another Access database, or another application's file. Like importing, changing the source data does not affect the exported data.

Each method has clear advantages and disadvantages, as covered in the following sections.

Linking between Access and external data is discussed in Chapter 7.

# When to link to external data

Linking in Access enables you to work with the data in another application's format—thus, sharing the file with the existing application. If you leave data in another database format, Access can read the data while the original application is still using it. This capability is useful when you want to work with data in Access that other programs also need to work with. However, there are limitations as to what you can do with linked data. For example, you can't update data in a linked Excel spreadsheet or a linked text file. The ability to work with external data is also useful when you use Access as a front end for a SQL Server database—you can link to a SQL Server table and directly update the data, without having to batch-upload it to the SQL Server.

Access databases are often linked to external data so that people can use Access forms to add and update the external data or to use the external data in Access reports.

You can link to the following types of data in Access:

+   - Other Access tables (ACCDB, ACCDE, ACCDR, MDB, MDA, MDE)
+   - Excel spreadsheets
+   - Outlook folders
+   - Text files
+   - XML files
+   - HTML documents
+   - SharePoint lists
+   - ODBC databases

> **CAUTION**
> Access is capable of linking to certain formats (like HTML tables, text files, Excel files, and XML documents) for read-only access. You can use and look at tables in HTML or text format; however, the tables can't be updated and records can't be added to them using Access.

A big disadvantage of working with linked tables is that you lose the capability to enforce referential integrity between tables (unless all the linked tables are in the same external Access database or all are in some other database management system that supports