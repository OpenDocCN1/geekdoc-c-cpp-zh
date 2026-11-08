# # Chapter 1 – A Closer Look on Relational Model

The Structured Query Language, or SQL, was originally designed for relational model. It is the language used to define the relationships between multiple data. It is also the database programming language used to query data in a relational schema.

So when did this all began?

The first relational database was created in the 60s and the programming in this model were primarily defined by mathematics. In fact, this model of database was based on Tuple Relational Calculus and Relational Algebra.

Don’t worry, though, there is no need for you to jump into algebra and calculus to handle relational databases. SQL will make relational database programming easier.

# ## Tables, Columns, and Rows

In the relational database, the data is stored in a table. In this model, all tables have names. For instance, you may name a table as “people” while you may name another table as “sales”. These names refer to the kind of data stored inside the table. In other words, the table we call “people” contains data of people while the table we call “sales” contains data of sales.

Every table features a set of columns. These columns define the different pieces of data within the table. This what makes the relational model different from other types of databases. You will notice that there are some databases that store data altogether. In a relational model, however, all data is separated by columns and each column has a name. Each column can also restrict the category and size of data that will be added in it. For instance, some columns can only store strings while some columns can only store numbers. The restriction assigned to each column depends on the creator of the database.

Columns are also categorized by being required and not required. A required column means that every row in the table must have a data which corresponds to what the column requires. A not required column, on the other hand, means that we can assert a NULL value for each row under that column. As you go through SQL, you will find that NULL has a lot uses in database programming.

The primary point of using rows is to have retrievable data and containers where you can store data. Why do we store data? Simply because we want to get that data again in the