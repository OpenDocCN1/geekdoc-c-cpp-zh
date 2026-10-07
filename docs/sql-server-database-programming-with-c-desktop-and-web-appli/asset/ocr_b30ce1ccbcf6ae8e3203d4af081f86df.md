# 2.8.2.1 Data Files

A data file is a conglomeration of objects, which includes tables, keys, views, stored procedures and others. All these are necessary for the efficient operation of the database.

# 2.8.2.2 Tables

The data in a relational database resides in tables, which are the building blocks of the database. Each table consists of columns and rows. Columns represent various attributes or fields in a table. Each row represents one record. For example, record in the Faculty table contains of name, office, phone, title, and email. Each field has a distinct type, meaning that it can contain only one type of data such as numeric or character. Tables are the first objects created in a database.

# 2.8.2.3 Views

Views are virtual tables, meaning that they do not contain any data. They are stored as queries in the database, which are executed when needed. A view can contain data from one or more tables. The views can provide database security. Sensitive information in a database can be excluded by including non-sensitive information in a view and providing access to the views instead of all tables in a database. The views can also hide the complexities of a database. A user can be using a view that is made up of multiple tables, whereas it appears as a single table to the user. The user can execute queries against a view just like a table.

# 2.8.2.4 Stored Procedures

Users use queries to retrieve, display or manipulate data in the database. These queries can be stored on the client machine or on the server. There are advantages associated with stored SQL queries on the server rather than on the client machine. The network performance. Usually, users use same queries over and over again; frequent, different users are trying to access the same data. Instead of sending the same queries over the network repeatedly, it improves the network performance and executes queries faster if the queries are stored on the server where they are compiled and saved as stored procedures. The users can simply call the stored procedure with a simple command like execute stored_procedure A.

# 2.8.2.5 Keys and Relationships

A primary key is created for each table in the database to efficiently access records and to ensure entity integrity. This implies that each record in a table is unique in some way. Therefore no two records can have the same primary key. It is defined as a unique identifier. Moreover a primary key may not have null value, i.e there may be missing data. SQL server creates a unique index for each primary key. This ensures the fast access to data. Or columns can be combined to designate a primary key.

In a relational database, relationships between tables can be logically defined with the help of foreign keys. A foreign key of one record in a table points specifically to a primary key of a record in another table. This allows a user to join multiple tables and retrieve information from more at a time. Foreign keys also enforce referential integrity, a defined relationship between the tables which does not allow insertion or deletion of records in a table unless the foreign key of a record in one table matches a primary key of another table. In other words, a record in one table cannot have a foreign key that does not point to a primary key in another table. Additionally a primary key may not be deleted if there are foreign keys in another table pointing to it. The foreign key values associated with a primary key must be deleted first. Referential integrity protects related data, from corruption, stored in different tables.

# 2.8.2.6 Indexes

The indexes are used to find records, quickly and efficiently, in a table just like one would use an index in a book. SQL server uses two types of indexes to retrieve and update data – clustered and non-clustered.