
## When to Index Tables

Unique: When set to Yes, the index must be unique within a table. A Social Security number field is a good candidate for a unique index because the application’s business rules may require one and only one instance of a Social Security number in the table. In contrast, a last name field should not be uniquely indexed, because many last names, like Smith and Jones, are very common, and having a unique index on the last name field will only cause problems. When applied to composite keys, the combination of field values must be unique—each field within the composite key can duplicate field values found within the table.

Ignore Nulls: If a record’s index field contains a null value (which happens in a composite index only if all fields in the composite index are null) the record’s index won’t contribute anything to the overall indexing. In other words, unless a record’s index contains some kind of value, Access doesn’t know where to insert the record in the table’s internal index sort lists. Therefore, you might want to instruct Access to ignore a record if the index value is null. By default, the Ignore Nulls property is set to No, which means Access inserts records with a Null index value into the indexing scheme along with any other records containing Null index values.

You should test the impact of the index properties on your Access tables and use the properties that best suit the data handled by your databases.

A field can be both the primary key for a table and part of a composite index. You should index your tables as necessary to yield the highest possible performance without worrying about over-indexing or violating some arcane indexing rules. For example, in a database such as Collectible Mini Cars, the invoice number in tblSales is frequently used in forms and reports and should be indexed. In addition, there are many situations in which the invoice number is used in combination with other fields, such as the sales date or salesperson ID. You should consider adding composite indexes combining the invoice number with sales date, and salesperson ID, to the sales table.

Depending on the number of records in a table, the extra overhead of maintaining an index may not justify creating an index beyond the table’s primary key. Though data retrieval is somewhat faster than it is without an index, Access must update index information whenever you enter or change records in the table. In contrast, changes to nonindexed fields do not require extra file activity. You can retrieve data from nonindexed fields as easily (although not as quickly) as from indexed fields.

Generally, it’s best to add secondary indexes when tables are quite large and when indexing fields other than the primary key speeds up searches. Even with large tables, however, indexing can slow performance if the records in tables will be changed often or new records will be added frequently. Each time a record is changed or added, Access must update all indexes in the table.

Given all the advantages of indexes, why not index everything in the table? What are the drawbacks of indexing too many fields? Is it possible to over-index tables?

First, indexes increase the size of the Access database somewhat. Unnecessarily indexing a table that doesn't really require an index eats up a bit of disk space for each record in the table. More important, indexes extract a performance hit for each index on the table every time a record is added to the table. Because Access automatically updates indexes each time a record is added (or removed), the internal indexing must be adjusted for each new record. If you have ten indexes on a table, Access makes ten adjustments to the indexes each time a new record is added or an existing record is deleted, causing a noticeable delay on large tables (particularly on slow computers).

Sometimes changes to the data in records cause adjustments to the indexing scheme. This is true if the change causes the record to change its position in sorting or query activities. Therefore, if you're working with large, constantly changing data sets that are rarely searched, you may choose not to index the fields in the table, or to minimally index by indexing only those few fields that are likely to be searched.

As you begin working with Access tables, you'll probably start with the simplest one-field indexes and migrate to more complex ones as your familiarity with the process grows. Keep in mind, however, the trade-offs between greater search efficiency and the overhead incurred by maintaining a large number of indexes on your tables.

It's also important to keep in mind that indexing does not modify the physical arrangement of records in the table. The natural order of the records (the order in which the records were added to the table) is maintained after the index is established.

> **NOTE**
> A compact and repair cycle on an Access database forces Access to rebuild the indexes in all the tables, and physically rearranges tables in primary key order in the ACCDB file. The maintenance operations ensure that your Access databases operate at maximum efficiency. See Chapter 31 for more on the Compact and Repair utility.

## Printing a Table Design

You can print a table design by clicking the Database Documenter button in the Analyze group on the Database Tools tab of the Ribbon. The Analyze group contains a number of tools that make it easy to document your database objects. When you click the Database Documenter button, the Documenter dialog box appears, letting you select objects to print. In Figure 3.19, tblCustomers is selected on the Tables tab of the Documenter dialog box.

You can also set various options for printing. When you click the Options button, the Print Table Definition dialog box (shown in Figure 3.20) appears, enabling you to select which information from the Table Design to print. You can print the various field names, all their properties, the indexes, and even network permissions.

### Part II: Understanding Access Tables

#### Figure 3.19
The Documenter dialog box.

![](img/1e45673ab6eca9d20e67635ff5b9b318_123_0.png)

#### Figure 3.20
Printing options in the Print Table Definition dialog box.

![](img/1e45673ab6eca9d20e67635ff5b9b318_123_1.png)

> **CAUTION**
> Don't select too many options in the Print Table Definition dialog box. Printing every detail of a table's design can take many pages to output. It's probably best to print just a few items for a table, and add to the options when necessary.

After you select the options you want, Access generates a report. You can view the report in a Print Preview window or send it to a printer. You may want to save the report within the database as part of the application’s documentation.

> **Tip**
> The Database Documenter creates a table of all the objects and object properties you specify. You can use this utility to document such database objects as forms, queries, reports, macros, and modules.

## Saving the Completed Table

You can save the completed table design by choosing File → Save or by clicking the Save button on the Quick Access toolbar in the upper-left corner of the Access environment. If you’re saving the table for the first time, Access asks for its name. Table names can be up to 64 characters long and follow standard Access object naming conventions: They may include letters and numbers, can’t begin with a number, and can’t include punctuation. If you try to close an unsaved table, Access will prompt you to save it.

If you’ve saved this table before and want to save it with a different name, choose File → Save As → Save Object As, click the Save As button, and enter a different table name. This action creates a new table design and leaves the original table with its original name untouched. If you want to delete the old table, select it in the Navigation pane and press the Delete key.

## Manipulating Tables

As you add many tables to your database, you may want to use them in other databases or make copies of them as backups. In many cases, you may want to copy only the table’s design and not include all the data in the table. You can perform many table operations in the Navigation pane, including:

- Renaming tables
- Deleting tables
- Copying tables in a database
- Copying a table to another database

You perform these tasks by direct manipulation or by using menu items.

### Renaming Tables

Rename a table by right-clicking its name in the Navigation pane and selecting Rename from the shortcut menu or by selecting the table in the Navigation pane and pressing the F2 key. After you change the table name, it appears in the Tables list, which re-sorts the tables in alphabetical order.
