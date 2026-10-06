
# Oracle SQL Developer Modeler for Database Design Mastery

To create a new trigger, go to the physical model's Browser pane, select the table or view name you want to add the trigger for, go to Triggers, right-click, and choose New. For a trigger, you define properties on four tabs: General, Trigger Body, Update Columns, and Comments. On the General tab, you define the name for the trigger and the schema owner (User) and the action that will invoke it (Insert/or Update and/or Delete). You also specify the triggering time (Before/After), the scope (for each row, for each statement), and the state (enable/disable). You can also define the names for old parameters (Ref OLD as), new parameters (Ref NEW as), and parent parameters (Ref PARENT as) and the Condition. On the Trigger Body tab, you can write the actual PL/SQL code for the trigger action, and on the Update Columns tab, you can select or remove columns to be updated if the action for the trigger is Update. On the Comments tab, you can document the trigger.

## User-Defined Data Types

You are not able to create data types in the physical model, but the collection types and structured types you might have defined early in the data types model will be automatically brought to the physical model.

You are able to change the name of a collection type and define the settings Owner, Force Place (NO/YES), OID (Object Identifier), and Comments for it. You can also define privileges by clicking the Permissions button.

You can also rename a structured type and define the settings Owner, Force Place (NO/YES), Global ID, Invoker Rights (empty, Current_user, Defined), Map Order Functions, Map To Java Class (NO/YES), and Comments for it. You can also define privileges by clicking the Permissions button.

## Other Elements

If you want to have the whole database designed and documented in Data Modeler, you can do that. You can add a database with its properties to the physical model to get the DDLs for it. In Database Properties, you can define properties on the General, Logging, and Tablespaces, and you can write comments. After defining the database for the physical model, you can see in the Browser pane new branches for adding data files, redo log groups, and SYSAUX files to database.

You can define directories and disk groups, and you define contexts, which are sets of application-defined attributes that validate and secure an application. You can also create clusters. A cluster is a schema object that contains data from one or more tables. The data of a cluster is that the data are retrieved together saved close to each other to enable fast performance. All the tables in a cluster must have at least one column in common. An index cluster stores all the rows from all the tables that share the same cluster key, and a hash cluster stores rows that have the same hash value together. In the physical model, you can create a cluster and attach tables or materialized views in it on the Table/Materialized View Properties tabs of the Cluster Properties dialog.

## Chapter 6: Introducing Physical Database Design 159

## Propagating Properties

In most of the properties dialogs, you will see a Propagate Properties button. This is useful functionality when you have defined the properties for one kind of object and want to have the same property copied to other objects of the same type. For instance, you might have defined the properties for a table such as Tablespace, Logging, Storage, Row Dependency, Row Movement, and Permissions, and you want to have the same settings for another 25 tables. Instead of manually entering all this information for your 25 tables, you can use the Propagate Properties utility. After setting the properties wanted over one table, just click Propagate Properties. The Properties Propagation dialog opens when you can first select properties to propagate and then which objects these properties will be propagated. This tool will probably be yours or your DBA's favorite tool in the physical database design.

![](img/431f8ac8f273fa89a28377c500ed60d7_185_0.png)

> TIP
You can use the Propagate Properties button for copying privileges. You can define privileges for one table and click Propagate Properties to copy the same set of privileges to other tables.

## Indexing

An index is a database object that provides a quick lookup of the data in a database. There are different types of indexes for different kinds of searches. Usually an index is justified by its usage: the amount of data, how the data is mainly used (select/update/insert/delete), and the frequency of selects. If the amount of data is small, there is probably no need for an index. If the data is mostly inserted, updated, and deleted, it might not be a good idea to add an index because indexes make only selects faster while making other operations slower. If you have a query that is run only once a year, it might not be a good idea to have an index supporting it in the database for 12 months a year. An index is defined for a column or columns in a table, and it supports select queries only with those columns in the WHERE clause of the query. An index does not support all the queries, and it is not a silver bullet for performance.

## 160 Oracle SQL Data Modeler for Database Design Mastery

There are different kinds of indexes. The most common is a B-tree index (B-tree, B+-tree, B*-tree); for spatial data there is the R-tree index (R-tree, R+-tree, R*-tree), and there are the following: bitmap index, context index, multilevel index, hash index, function-based index, bitmap join, reverse index, and so on. A primary key has a special index called a primary index, and a table can have only one of them. Many indexes for foreign keys are created to support the joins and to avoid locking problems. To be able to decide about other possible indexes, you should research the most common queries and their frequency. In the physical model, you can create a cluster and attach tables or materialized views in it on the Table/Materialized View Properties tabs of the Cluster Properties dialog. (Wait, let's re-examine the OCR for page 186-187. The OCR seems to have become corrupted/garbled in the latter half. I will reconstruct the logical flow based on standard database design terminology).

*Self-correction: The OCR text for pages 186-187 is extremely repetitive and contains many errors (e.g., "index431f8ac8f273fa89a28377c500ed60d7_186_0"). I will clean up the text while maintaining the intended content.*

There are different kinds of indexes. The most common is a B-tree index (B-tree, B+-tree, B*-tree); for spatial data there is the R-tree index (R-tree, R+-tree, R*-tree), and there are the following: bitmap index, context index, multilevel index, hash index, function-based index, bitmap join, reverse index, and so on. A primary key has a special index called a primary index, and a table can have only one of them. Many indexes for foreign keys are created to support the joins and to avoid locking problems. To be able to decide about other possible indexes, you should research the most common queries and their frequency.

## Chapter 6: Introducing Physical Database Design 161

## Partitioning

If a table, or materialized view is big, it is possible to partition it. Partitioning in Oracle requires the partitioning option that is available for Enterprise Edition. Partitioning makes maintaining easier and improves the performance. In my opinion, the main advantage of partitioning is the maintenance, and second is the improvement on performance. For instance, partitioning makes deleting fast; you can just drop a partition. If you decide to use partitioning, carefully consider the possibilities your RDBMS has and design partitioning carefully.

Partitioning operation affects only the physical schema. That means the logical model (and relational model) stay untouched, and no programs need to be changed. Some partitioning may need some extra columns to get a working partition key, and then the logical model and programs must be changed.

You can create a new partition in the physical model in the Browser pane; under the table you want to create, right-click, and choose New. There are five tabs: General, Subpartition Order, Subpartitions, Local Index, and Comments. On the General tab you can specify the following settings: Name, List (free text edit), Tablespace (from the list of tablespaces), Logging (null, YES, NO), Storage (select from the list of storage templates), and Data Compression (null, YES, NO). For a table in Table Properties, you set the Partition property to YES, and on the Partitioning tab you select the partition type and if needed the subpartition type. After selecting the subpartition type for the table, you can create a new subpartition of the selected type (Hash, List, Range) and specify the parameters needed for the DDL. In Browser pane (under the table) you can also define a storage template and LOB storage for a subpartition.
