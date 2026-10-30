Now that you know some basics about data access, it's time to consider multiple tables and/or multiple queries in a DataSet. This chapter examines techniques for establishing relationships among tables and extracting data from the tables.

# Data Relationships

In relational databases, the data items are generally stored in multiple related tables. The primary table is called the parent or master table and the second table is the child or detail table. The relationship between two tables may be one-to-one (1:1), one-to-many (1:M), or many-to-many (M:N). Each table usually has a field or fields, called the primary key, that uniquely identify each record. When the primary key of one table is included as a field in a related table to link the two tables, that field is called a foreign key. The foreign key is common to both tables.

# One-to-Many Relationships

The most common type of relationship is one-to-many: one record in the parent table relates to one or more records in the child table. Examples include a customer with multiple orders, a department with multiple employees, or a student with multiple courses. In a one-to-many relationship, a row in the parent table can have many matching rows in the child table, but a row in the child table has only one matching record in the parent.

Figure 4.1 shows a database diagram of a 1:M relationship, using the stores and sales tables of the Pubs database. Figure 4.2 shows some sample data from the two tables. You can see that one store can have many sales, but each sale has only one store.

# Many-to-Many Relationships

Another possible relationship is many-to-many. An example in the Pubs database is titles and authors. One author can write many books and one book can have many authors. Most database management systems, including SQL Server and Access, cannot directly handle many-to-many relationships. Instead, a third table is needed to join the two tables. In the third table, called a junction table, the primary key consists of the foreign keys from both tables. In Pubs, the junction table is called titleauthors and contains title_id and au_id columns.

![](bbox=[0.25, 0.88, 0.55, 0.98])

# Figure 4.1

A database diagram of a 1:M relationship.