
speed of queries. Celko mentions that the process of joining multiple tables in a fully normalized database is costly, specifically affecting processing time and computer resources.

## Normalization Strategies

After transforming entities and attributes from the conceptual design into a logical design, the tables and columns are created. This is when a process known as normalization occurs. Normalization refers to the process of making your database tables subscribe to certain rules. Many, if not most, database designers are satisfied when third normal form (3NF) is achieved and, for the objectives of this book, I will stop at 3NF, too. To help explain the various normalization steps, an example scenario follows.

### First Normal Form (1NF)

First normal form (1NF) involves the elimination of data redundancy or repeating information from a table. A table is considered to be in first normal form when all of its columns describe the table completely and when each column in a row has only one value. A table satisfies 1NF when each column in a row has a single value and no repeating group information. Essentially, every table meets 1NF as long as an array, list, or other structure has not been defined. The following table illustrates a table satisfying the 1NF rule because it has only one value at each row-and-column intersection. The table is in ascending order by CUSTNUM and consists of customers and the purchases they made at an office supply store.

Table 1.1: First Normal Form (1NF) Table

| CUSTNUM | CUSTNAME | CUSTCITY | ITEM | UNITS | UNITCOST | MANUCITY |
|---|---|---|---|---|---|---|
| 1 | Smith | San Diego | Chair | 1 | $179.00 | San Diego |
| 1 | Smith | San Diego | Pens | 12 | $0.89 | Los Angeles |
| 1 | Smith | San Diego | Paper | 4 | $6.95 | Washington |
| 1 | Smithe | San Diego | Stapler | 1 | $8.95 | Los Angeles |
| 7 | Lafler | Spring Valley | Mouse Pad | 1 | $11.79 | San Diego |
| 7 | Loffler | Spring Valley | Pens | 24 | $1.59 | Los Angeles |
| 13 | Thompson | Miami | Markers | . | $0.99 | Los Angeles |

### Second Normal Form (2NF)

Second normal form (2NF) addresses the relationships between sets of data. A table is said to be in second normal form when all the requirements of 1NF are met and a foreign key is used to link any data in one table which has relevance to another table. The very nature of leaving a table in first normal form (1NF) may present problems due to the repetition of some information in the table. One noticeable problem is that Table 1.1 has repetitive information in it. Another problem is that there are misspellings in the customer name. Although repeating information may be permissible with hierarchical file structures and other legacy type file structures, it does pose a potential data consistency problem as it relates to relational data.

To describe how data consistency problems can occur, let’s say that a customer takes a new job and moves to a new city. In changing the customer’s city to the new location, it would be very easy to miss one or more occurrences of the customer’s city resulting in a customer residing incorrectly in two different cities. Assuming that our table is only meant to track one unique customer per city, this would definitely be a data consistency problem. Essentially, second normal form (2NF) is important because it says that every non-key column must depend on the entire primary key.

Tables that subscribe to 2NF prevent the need to make changes in more than one place. What this means in normalization terms is that tables in 2NF have no partial key dependencies. As a result, our database that consists of a single table that satisfies 1NF will need to be split into two separate tables in order to subscribe to the 2NF rule. Each table would contain the CUSTNUM column to connect the two tables. Unlike the single table in 1NF, the tables in 2NF allow a customer’s city to be easily changed whenever they move to another city because the CUSTCITY column only appears once. The tables in 2NF would be constructed as follows.

Table 1.2: CUSTOMERS Table

| CUSTNUM | CUSTNAME | CUSTCITY |
|---|---|---|
| 1 | Smith | San Diego |
| 1 | Smithe | San Diego |
| 7 | Lafler | Spring Valley |
| 13 | Thompson | Miami |

Table 1.3: PURCHASES Table

| CUSTNUM | ITEM | UNITS | UNITCOST | MANUCITY |
|---|---|---|---|---|
| 1 | Chair | 1 | $179.00 | San Diego |
| 1 | Pens | 12 | $0.89 | Los Angeles |
| 1 | Paper | 4 | $6.95 | Washington |
| 1 | Stapler | 1 | $8.95 | Los Angeles |
| 7 | Mouse Pad | 1 | $11.79 | San Diego |
| 7 | Pens | 24 | $1.59 | Los Angeles |
| 13 | Markers | . | $0.99 | Los Angeles |

### Third Normal Form (3NF)

Referring to the two tables constructed according to the rules of 2NF, you may have noticed that the PURCHASES table contains a column called MANUCITY. The MANUCITY column stores the city where the product manufacturer is headquartered. Keeping this column in the PURCHASES table violates the third normal form (3NF) because MANUCITY does not provide factual information about the primary key column (CUSTNUM) in the PURCHASES table. Consequently, tables are considered to be in third normal form (3NF) when each column is dependent on the key, the whole key, and nothing but the key. The tables in 3NF are constructed so the MANUCITY column would be in a table of its own as follows.

Table 1.4: CUSTOMERS Table

| CUSTNUM | CUSTNAME | CUSTCITY |
|---|---|---|
| 1 | Smith | San Diego |
| 1 | Smithe | San Diego |
| 7 | Lafler | Spring Valley |
| 13 | Thompson | Miami |

Table 1.5: PURCHASES Table

| CUSTNUM | ITEM | UNITS | UNITCOST |
|---|---|---|---|
| 1 | Chair | 1 | $179.00 |
| 1 | Pens | 12 | $0.89 |
| 1 | Paper | 4 | $6.95 |
| 1 | Stapler | 1 | $8.95 |
| 7 | Mouse Pad | 1 | $11.79 |
| 7 | Pens | 24 | $1.59 |
| 13 | Markers | . | $0.99 |

Table 1.6: MANUFACTURERS Table

| MANUNUM | MANUCITY |
|---|---|
| 101 | San Diego |
| 112 | San Diego |
| 210 | Los Angeles |
| 212 | Los Angeles |
| 213 | Los Angeles |
| 214 | Los Angeles |
| 401 | Washington |

### Beyond Third Normal Form

In general, database designers are satisfied when their database tables subscribe to the rules in 3NF. But, it is not uncommon for others to normalize their database tables to fourth normal form (4NF) where independent one-to-many relationships between primary key and non-key columns are forbidden. Some database purists will even normalize to fifth normal form (5NF) where tables are split into the smallest pieces of information in an attempt to eliminate any and all table redundancies. Although constructing tables in 5NF may provide the greatest level of database integrity, it is neither practical nor desired by most database practitioners.

There is no absolute right or wrong reason for database designers to normalize beyond 3NF as long as they have considered all the performance issues that may arise by doing so. A common problem that occurs when database tables are normalized beyond 3NF is that a large number of small tables are generated. In these cases, an increase in time and computer resources frequently occurs because small tables must first be joined before a query, report, or statistic can be produced.

## Column Names and Reserved Words

According to the American National Standards Institute (ANSI), SQL is the standard language used with relational database management systems. The ANSI Standard reserves a number of SQL keywords from being used as column names. The SAS SQL implementation is not as rigid, but users should be aware of what reserved words exist to prevent unexpected and unintended results during SQL processing. Column names should conform to proper SAS naming conventions (as described in the *SAS Language Reference*), and they should not conflict with certain reserved words found in the SQL language. The following list identifies the reserved words found in the ANSI SQL standard.

### ANSI SQL Reserved Words

|  |  |  |
|---|---|---|
| AS | INNER | OUTER |
| CASE | INTERSECT | RIGHT |
| EXCEPT | JOIN | UNION |
| FROM | LEFT | UPPER |
| FULL | LOWER | USER |
| GROUP | ON | WHEN |
| HAVING | ORDER | WHERE |

You probably will not encounter too many conflicts between a column name and an SQL reserved word, but when you do you will need to follow a few simple rules to prevent processing errors from occurring. As was stated earlier, although PROC SQL’s naming conventions are not as rigid as other vendor’s implementations, care should still be exercised, in particular when PROC SQL code is transferred to other database environments expecting it to run error free. If a column name in an existing table conflicts with a reserved word, you have three options at your disposal:

- 1. Physically rename the column name in the table, as well as any references to the column.
- 2. Use the RENAME= data set option to rename the desired column in the current query.
- 3. Specify the PROC SQL option DQUOTE=ANSI, and surround the column name (reserved word) in double quotes, as illustrated below.

### SQL Code

```sql
PROC SQL DQUOTE=ANSI;
    SELECT *
        FROM RESERVED_WORDS
        WHERE "WHERE"='EXAMPLE';
QUIT;
```

## Data Integrity

*Webster’s New World Dictionary* defines *integrity* as “the quality or state of being complete; perfect condition; reliable; soundness.” Data integrity is a critical element that every organization must promote and strive for. It is imperative that the data tables in a database environment be reliable, free of errors, and sound in every conceivable way. The existence of data errors, missing information, broken links, and other related problems in one or more tables can impact decision-making and information reporting activities resulting in a loss of confidence among users.
