| ID | Name | Department | Salary | Location |
|---:|---|---:|---:|---|
| 23603 | Jones | 413 | 1100 | New Jersey |
| 24568 | Kerwin | 413 | 2000 | New Jersey |
| 34589 | Larson | 642 | 1800 | Los Angeles |
| 35761 | Myers | 411 | 1400 | Orlando |
| 47132 | Neumann | 413 | 9000 | New Jersey |
| 78321 | Stephens | 611 | 8500 | Orlando |

_Row_ — Primary key: ID; _Column_ — Department

**Fig. 20.1** | Employees table sample data.

Rows in Fig. 20.1 are displayed in *ascending* order by primary key. But they could be listed in *descending* order or in no particular order at all.

Each column represents a different data *attribute*. Some column values may be duplicated between rows. For example, three different rows in the Employees table’s Department column contain the number 413, indicating that these employees work in the same department.

# *Selecting Data Subsets*

You can use LINQ to Entities to define queries that select subsets of the data from a table. For example, a program might select data from the Employees table to create a query result that shows where each department is located, in ascending order by Department number (Fig. 20.2).

| Department | Location |
|---:|---|
| 413 | New Jersey |
| 611 | Orlando |
| 642 | Los Angeles |

**Fig. 20.2** | Distinct Department and Location data from the Employees table.

# 20.3 A Books Database

We now consider a simple Books database that stores information about some Deitel books. First, we overview the database’s tables. A database’s tables, their fields and the relationships among them are collectively known as a database schema. The ADO.NET Entity Framework uses a database’s schema to define classes that enable you to interact with the database. Sections 20.5–20.8.2 show how to manipulate the Books database. The database file—Books.mdf—is provided with this chapter’s examples. SQL Server database files have the .mdf (“master data file”) filename extension.

# *Authors Table*

The database consists of three tables: Authors, Titles and AuthorISBN. The Authors table (described in Fig. 20.3) consists of three columns that maintain each author’s unique