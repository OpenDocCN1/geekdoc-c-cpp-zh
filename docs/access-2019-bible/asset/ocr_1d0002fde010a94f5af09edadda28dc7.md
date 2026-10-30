referential integrity). Linked tables may exhibit somewhat poorer performance than local tables. Depending on the source and the location of the source data, users might experience a noticeable delay when they open a form or report that is based on linked data.

Performance issues become more pronounced when joining linked and local data in a query. Because Access is unable to apply optimization techniques to foreign data, many joins are inefficient and require more memory and CPU time to complete than joining local tables. However, Access can work with many different types of external data, which makes it the ideal platform for applications requiring those features.

# When to import external data

Importing data enables you to bring an external table or data source into a new or existing Access table. By importing data, Access automatically converts data from the external format and copies it into Access. You can even import data objects into a different Access database or Access project from the one that is currently open. If you know that you'll use your data in Access only, you should import it. Generally, Access works faster with its own local tables.

> **NOTE**
> 
> Because importing makes another copy of the data, you might want to delete the old file after you import the copy into Access. Sometimes, however, you'll want to preserve the old data file. For example, the data might be an Excel spreadsheet still in use. In such cases as this, simply maintain the duplicate data and accept that storing it will require more disk space (and that the two files are going to get out of sync).

One of the principal reasons to import data is to customize it to meet your needs. After a table has been imported into an Access database, you can work with the new table as if you'd built it in the current database. With linked tables, on the other hand, you're greatly limited in the changes you can make. For example, you can't specify a primary key or assign a data entry rule, which means that you can't enforce integrity against the linked table. Also, because linked tables point to external files, which Access expects to find in a specific location, it can make distributing your application more difficult.

Data is frequently imported into an Access database from an obsolete system being replaced by a new Access application. When the import process is complete, the obsolete application can be removed from the user's computer.

> **TIP**
> 
> If you'll be importing data from the same source frequently, you can automate the process with a macro or a VBA procedure. This can be helpful for those times when you have to import data from an external source on a regular schedule or when you have complex transformations that must be applied to the imported data.