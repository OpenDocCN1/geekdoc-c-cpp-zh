# Relationships Between Tables

The lines connecting the tables in Fig. 20.9 represent the relationships among the tables. Consider the line between the Authors and AuthorISBN tables. On the Authors end of the line, there's a 1, and on the AuthorISBN end, an infinity symbol (∞). This indicates a one-to-many relationship—for each author in the Authors table, there can be an arbitrary number of ISBNs for books written by that author in the AuthorISBN table (that is, an author can write any number of books). Note that the relationship line links the AuthorID column in the Authors table (where AuthorID is the primary key) to the AuthorID column in the AuthorISBN table (where AuthorID is a foreign key)—the line between the tables links the primary key to the matching foreign key.

The line between the Titles and AuthorISBN tables illustrates a one-to-many relationship—one book can be written by many authors. Note that the line between the tables links the primary key ISBN in the Titles table to the corresponding foreign key in the AuthorISBN table. Figure 20.9 illustrates that the sole purpose of the AuthorISBN table is to provide a many-to-many relationship between the Authors and Titles tables—an author can write many books, and a book can have many authors.

# 20.4 LINQ to Entities and the ADO.NET Entity Framework

When using the ADO.NET Entity Framework, you interact with the database via classes that the IDE generates from the database schema. You'll initiate this process by adding a new ADO.NET Entity Data Model to your project (as you'll see in Section 20.5.1).

# Classes Generated in the Entity Data Model

For the Authors and Titles tables in the Books database, the IDE creates two classes each in the data model:

+   - The first class represents a row of the table and contains properties for each column in the table. Objects of this class—called row objects—store the data from individual rows of the table. The IDE uses the singular version of a table's plural name as the row class's name. For the Books database's Authors table, the row class's name is Author, and for the Titles table, it's Title.
+   - The second class represents the table itself. An object of this class stores a collection of row objects that correspond to all of the rows in the table. The table classes for the Books database are named Authors and Titles.

Once generated, the entity data model classes have full IntelliSense support in the IDE. Section 20.7 demonstrates queries that use the relationships among the Books database's tables to join data.

# Relationships Between Tables in the Entity Data Model

You'll notice that we did not mention the Books database's AuthorISBN table. Recall that this table links

+   - each author in the Authors table to that author's books in the Titles table, and
+   - each book in the Titles table to the book's authors in the Authors table.