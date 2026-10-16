
# Chapter 5: Creating, Populating, and Deleting Tables

Introduction ........................................................................................ 164
Creating Tables................................................................................................ 164
  Creating a Table Using Column-Definition Lists............................................... 165
  Creating a Table Using the LIKE Clause ........................................................... 169
  Deriving a Table and Data from an Existing Table............................................. 170
Populating Tables ............................................................................................ 172
  Adding Data to a Table with a SET Clause ....................................................... 173
  Adding Data to All of the Columns in a Row..................................................... 176
  Adding Data to Some of the Columns in a Row ................................................ 181
  Adding Data with a SELECT Query.................................................................... 185
  Bulk Loading Data from Microsoft Excel ........................................................... 186
Integrity Constraints ....................................................................................... 192
  Defining Integrity Constraints........................................................................... 192
  Types of Integrity Constraints........................................................................... 192
  Preventing Null Values with a NOT NULL Constraint ....................................... 192
  Enforcing Unique Values with a UNIQUE Constraint........................................... 195
  Validating Column Values with a CHECK Constraint ....................................... 196
  Referential Integrity Constraints...................................................................... 197
  Establishing a Primary Key............................................................................... 198
  Establishing a Foreign Key ............................................................................... 199
  Displaying Integrity Constraints....................................................................... 202
Deleting Rows in a Table.................................................................................. 203
  Deleting a Single Row in a Table....................................................................... 203
  Deleting More Than One Row in a Table........................................................... 204
  Deleting All Rows in a Table ............................................................................ 204
Deleting Tables ................................................................................................ 205
  Deleting a Single Table..................................................................................... 205
  Deleting Multiple Tables................................................................................... 206
  Deleting Tables That Contain Integrity Constraints........................................... 206
Summary ........................................................................................................... 208

## Introduction

Previous chapters provided tables in the examples that had already been created and populated with data. But what if you need to create a table, populate it with data, or delete rows of data or tables that are no longer needed or wanted?

In this chapter, the discussions and examples focus on the way tables are created, populated, and deleted. These are important operations and essential elements in PROC SQL, especially if you want to increase your comprehension of SQL processes and improve your understanding of this powerful language.

## Creating Tables

An important element in table creation is table design. Table design incorporates how tables are structured—how rows and columns are defined, how indexes are created, and how columns refer to values in other columns. If you seek a greater understanding in this area, then review the many references identified at the end of this book. The following overview should be kept in mind during the table design process.

When building a table it is important to devote adequate time to planning its design as well as understanding the needs that each table is meant to satisfy. This process involves a number of activities such as requirements and feasibility analysis, including cost/benefit of the proposed tables, the development of a logical description of the data sources, and physical implementation of the logical data model. Once these tasks are complete, you can assess any special business requirements that each table needs to provide. A business assessment helps by minimizing the number of changes required to a table once it has been created.

Next, determine what tables will be incorporated into your application’s database. This requires understanding the value that each table is expected to provide. It also prevents a table of little or no importance from being incorporated into a database. The final step and one of critical importance is to define each table’s columns, attributes, and contents.

Once the table design process is complete, each table is then ready to be created with the CREATE TABLE statement. The purpose of creating a table is to create an object that does not already exist. In the SAS implementation, three variations of the CREATE TABLE statement can be specified depending on your needs:

- Creating a table using column-definition lists
- Creating a table using the LIKE clause
- Deriving a table and data from an existing table

### Creating a Table Using Column-Definition Lists

Although part of the SQL standard, the column-definition list (like the LENGTH statement in the DATA step) is a laborious and not very elegant way to create a table. The disadvantage of creating a table this way is that it requires the definition of each column’s attributes including their data type, length, informat, and format. This method is frequently used to create columns when they are not present in another table. Using this method results in the creation of an empty table (without rows). The code used to create the CUSTOMERS table appears below. This example illustrates the creation of a table with column-definition lists.

#### SQL Code

```
PROC SQL;
    CREATE TABLE CUSTOMERS
        (CUSTNUM    NUM        LABEL='Customer Number',
         CUSTNAME   CHAR(25)   LABEL='Customer Name',
         CUSTCITY   CHAR(20)   LABEL='Customer''s Home City');
QUIT;
```

#### SAS Log Results

```
PROC SQL;
    CREATE TABLE CUSTOMERS
        (CUSTNUM    NUM        LABEL='Customer Number',
         CUSTNAME   CHAR(25)   LABEL='Customer Name',
         CUSTCITY   CHAR(20)   LABEL='Customer''s Home City');
NOTE: Table CUSTOMERS created, with 0 rows and 3 columns.
    QUIT;
NOTE: PROCEDURE SQL used:
    real time          0.81 seconds
```

You should be aware that the SQL procedure ignores width specifications for numeric columns. When a numeric column is defined, it is created with a width of 8 bytes, which is the maximum precision allowed by SAS. PROC SQL ignores numeric length specifications when the value is less than 8 bytes. To illustrate this point, a partial CONTENTS procedure output is displayed for the CUSTOMERS table.

#### Results

![](img/9d3e4d8fa063e50a0c9985e34cf9d6e8_188_0.png)

| Alphabetic List of Variables and Attributes |
|---|---|---|---|
| # | Variable | Type | Len | Label |
| 3 | CUSTCITY | Char | 20 | Customer's Home City |
| 2 | CUSTNAME | Char | 25 | Customer Name |
| 1 | CUSTNUM | Num | 8 | Customer Number |

To conserve storage space (CUSTNUM only requires maximum precision provided in 3 bytes), a LENGTH statement could be used in a DATA step to define CUSTNUM as a 3-byte column rather than an 8-byte column.

#### DATA Step Code

```
DATA CUSTOMERS;
    LENGTH CUSTNUM 3.;
    SET CUSTOMERS;
    LABEL CUSTNUM = 'Customer Number';
RUN;
```
