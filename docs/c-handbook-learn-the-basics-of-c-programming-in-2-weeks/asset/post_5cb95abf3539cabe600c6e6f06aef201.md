
## How to Use the TOP Clause

The TOP clause allows you to retrieve a number or percentage from your data tables.

Important Note: Some databases are not compatible with this clause. For instance, MySQL uses LIMIT to retrieve records.

The syntax of a SELECT command with the TOP clause is:

```sql
SELECT TOP number|percent column_name(s)
FROM table_name
WHERE [condition]
```

## How to Sort Data

SQL offers ORDER BY, a clause that sorts data in descending or ascending order, depending on the column/s you use as a basis. The syntax that you should use is:

```sql
SELECT column-list
FROM table_name
[WHERE condition]
[ORDER BY column1, column2, .. columnN] [ASC | DESC];
```

You may include multiple columns in this clause. However, make sure that all of the columns you want to use are inside the column-list.

## How to Mix the Results of Multiple SELECT Commands

In SQL, you may combine results from multiple SELECT commands while preventing redundant rows. You just have to use the UNION clause.

To use this clause, your SELECT statements should have the same quantity of selected columns and column expressions. The statements must also have the same type of data and column arrangement. However, the statements don’t need to have identical lengths.

The syntax for this clause is:

```sql
SELECT column1 [, column2 ]
FROM table1 [, table2 ]
[WHERE condition]

UNION

SELECT column1 [, column2 ]
FROM table1 [, table2 ]
[WHERE condition]
```

## Chapter 8: How to Combine Records Using SQL

You may use the JOIN clause to combine records from multiple databases. Basically, JOIN is a method that can combine fields from different tables.

### The Different Types of JOIN

The SQL computer language supports different kinds of JOIN. These are:

- SELF JOIN – You can use this if you want to link a table to itself as if you are working on different tables. While doing this, you should rename at least one table in your SQL command.
- RIGHT JOIN – This JOIN retrieves all data rows from the right table. SQL will complete this task even if no matches exist between the two tables.
- LEFT JOIN – This JOIN returns all data rows from the left table. The SQL language will complete this even if no matches exist between the tables involved.
- FULL JOIN – This JOIN retrieves data rows if one of the tables has a match.
- INNER JOIN – This returns data rows if both tables have a match.
- CARTESIAN JOIN – This JOIN retrieves the Cartesian values of the record sets from the joined tables.

Let’s discuss each JOIN in detail:

### The INNER JOIN

This is one of the most important joins in SQL. It generates a new table by mixing the column values of different tables. The database query checks the rows of all tables to determine if there are row pairs that meet the join-predicate’s requirements. If the pairs of rows satisfy the join-predicate, the values for those rows are placed in a new table. Here’s the syntax that you should use:

```sql
SELECT table1.column1, table2.column2...
FROM table1
INNER JOIN table2
ON table1.common_field = table2.common_field;
```

### The LEFT JOIN

This JOIN retrieves all data rows from the left table. SQL does this even if the right table doesn’t have any match. Thus, if your command’s ON clause has 0 matches with the right table, you’ll still get a data row from the process. However, the columns from the right table will have NULL values inside them.

The syntax of this join is:

```sql
SELECT table1.column1, table2.column2...
FROM table1
LEFT JOIN table2
ON table1.common_field = table2.common_field;
```

### The RIGHT JOIN

This JOIN returns all data rows from the table on the right. The SQL language will do this even if the left table doesn’t have any match. Basically, you’ll still get at least one data row from this process even if your command’s ON clause has no matches with the left table. However, the columns from the left table will contain NULL values.

The syntax of this join is:

```sql
SELECT table1.column1, table2.column2...
FROM table1
RIGHT JOIN table2
ON table1.common_field = table2.common_field;
```

### The FULL JOIN

This SQL JOIN mixes the results of the left and right joins. The new table will have all of the records from the two tables. Here’s the syntax that you should use:

```sql
SELECT table1.column1, table2.column2...
FROM table1
FULL JOIN table2
ON table1.common_field = table2.common_field;
```

Important Note: FULL JOIN uses NULL values to fill records that don’t match.

### The SELF JOIN

You should use this join if you want to link a table to itself. As noted earlier, you have to rename at least one of the tables in your SQL statement.

The syntax of this JOIN is:

```sql
SELECT a.column_name, b.column_name...
FROM table1 a, table1 b
WHERE a.common_field = b.common_field;
```

### The CARTESIAN JOIN

This JOIN retrieves the Cartesian products of the record sets from the tables that you are using. Because of this, SQL users consider this as an INNER JOIN whose join-condition is always true. The syntax of the CARTESIAN JOIN is:

```sql
SELECT table1.column1, table2.column2...
FROM table1, table2 [, table3 ]
```

## Conclusion

Thank you again for downloading this book!

I hope this book was able to help you learn the basics of SQL in just two weeks.

The next step is to use this computer language in creating and managing your own databases.

Finally, if you enjoyed this book, then I’d like to ask you for a favor, would you be kind enough to leave a review for this book on Amazon? It’d be greatly appreciated!

[Click here to leave a review for this book on Amazon!](#)

Also be sure to signup for my technology and programming newsletter to get your FREE books and learn more about how to program. [Click Here](#).

Thank you and good luck!

**_[Click Here to get step by step instructions for setting up your Wordpress site with Bluehost.](#)_**

## Bonus: Receive More Free Books By Me!

Thanks for reading my book! I hope you received awesome value from it. I’d like to thank you by giving you more free books, and info related to programming and technology!

Simply click on the link below and enter your email address on my website!

Everything you will get will be useful to you if you’re serious about changing your programming skills. I will be offering:

- More Books By Me
- How I was able to learn programming in record time
- Info On My Favourite Products Related To Programming
- And Much More!

[Click Here to get access to all this info!](#)

If you haven’t already, be sure to check out my new website, *KindleBookSpot.com*. This is a new project I’ve been working on, and I really hope it’s valuable to my readers. I made the site because I wanted to give you guys an easier way to find the hottest kindle books at discounted prices, all in one place. Here are some details on what my site has:

- A list of best selling free kindle books
- Discounted fiction and non-fiction books
- A book of the week
- Featured books
- Promote your own book on my site

This site isn’t just for readers, it’s also a spot where up and coming authors can promote their new books before they turn to best sellers. So if you’d like to promote your own book, check out my site, *KindleBookSpot.com*.

I hope this site will be useful to you, and I hope to see you there!

Subscribe to our growing community at KindleBookSpot to receive notifications when the best books are discounted and free.

## Hacking Bootcamp

## Learn the Basics of Computer Hacking

*More discounted books at [kindlebookspot.com](https://kindlebookspot.com)*

## Table Of Content

- Introduction
- Chapter 1: Hacking – General Information
- Chapter 2: Programming Skills
- Chapter 3: Passwords
- Chapter 5: Penetration Testing
- Conclusion

## Introduction

I want to thank you and congratulate you for downloading the book, “ *Learn the Basics of Computer Hacking (Security, Penetration Testing, How to Hack)*.

This book contains proven steps and strategies on how to hack computer networks.

This e-book will teach you the basic ideas and concepts related to hacking. It will explain the tools, methods and techniques used by experienced hackers. By reading this material, you can conduct reconnaissance and software attacks against your target networks.

Thanks again for downloading this book, I hope you enjoy it!
