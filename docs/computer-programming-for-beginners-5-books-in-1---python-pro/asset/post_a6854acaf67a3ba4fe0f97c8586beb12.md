
enter in a column. This table definition generates a CHECK constraint and three columns:

```sql
CREATE TABLE BOOK_TITLES
( BOOK_ID     INT,
  BOOK_TITLE  CHARACTER (50) NOT NULL,
  STOCK_AVAILABILITY  INT,
  CONSTRAINT TS_STOCK_AVAILABILITY ( STOCK_AVAILABILITY < 50
  AND STOCK_AVAILABILITY > 1 ) ); ²¹
```

The resulting table will reject values that are outside the 1-50 range. Here's another way to write the table:

```sql
CREATE TABLE BOOK_TITLES
( BOOK_ID     INT,
  BOOK_TITLE  CHARACTER (50) NOT NULL,
  STOCK_AVAILABILITY  INT CHECK ( STOCK_AVAILABILITY < 50
  AND STOCK_AVAILABILITY > 1 ) );
```

Now, let's analyze the condition clause of these statements. This clause tells SQL that all of the values added to the STOCK_AVAILABILITY column must be lower than 50. The keyword AND informs SQL that there's another condition that must be applied. Finally, the clause tells SQL that each value added to the said column should be higher than 1. To put it simply, each value should be lower than 50 and higher than 1.

This constraint also allows you to simply list your “acceptable values.” SQL users consider this a powerful option when it comes to values that won't be changed regularly. In the next example, you will use the CHECK constraint to define a book's genre:

```sql
CREATE TABLE BOOK_TITLES
( BOOK_ID     INT,
  BOOK_TITLE  CHARACTER (50) ,
  GENRE       CHAR (10) ,
  CONSTRAINT TS_GENRE CHECK ( GENRE IN ( 'DRAMA', 'HORROR',
  'SELF HELP', 'ACTION', 'MYSTERY', 'ROMANCE' ) ) ); ²²
```

Each value inside the GENRE column should be included in the listed genres of the condition. As you can see, this statement uses IN (i.e. an SQL operator). Basically, IN makes sure that the values within GENRE are included in the listed entries.

This constraint can be extremely confusing since it involves a lot of parentheses. You may simplify your SQL codes by dividing them into multiple lines. As an example, let's rewrite the code given above:

```sql
CREATE TABLE BOOK_TITLES
(
BOOK_ID      INT,
BOOK_TITLE   CHAR (50) ,
GENRE        CHAR (10) ,
CONSTRAINT TS_GENRE CHECK
(
GENRE IN
( 'DRAMA', 'HORROR', 'SELF HELP', 'ACTION', 'MYSTERY', 'ROMANCE'
)
)
) ;
```

This style of writing SQL commands ensures code readability. Here, you need to indent the parentheses and their content so that they clearly show their position in the different layers of the SQL statement. By using this style, you can quickly identify the clauses placed in each pair of parentheses. Additionally, this statement works like the previous one. The only drawback of this style is that you need to use lots of spaces.

Let's analyze another example:

```sql
CREATE TABLE BOOK_TITLES
( BOOK_ID      INT,
  BOOK_TITLE   CHAR (50) ,
  STOCK_AVAILABILITY  INT,
  CONSTRAINT TS_STOCK_AVAILABILITY_CHECK ( ( STOCK_AVAILABILITY BETWEEN 1 AND 50 ) OR ( STOCK_AVAILABILITY BETWEEN 79 AND 90 ) ) );
```

This code uses BETWEEN (i.e. another SQL operator) to set a range that includes the lowest and highest points. Because it has two ranges, it separates the range specifications using parentheses. The OR keyword connects the range specifications. Basically, OR tells SQL that one of the conditions need to be satisfied. Consequently, the values you enter in the column named STOCK_AVAILABILITY should be from 1 through 50 or from 79 through 90.

## How to Define an Assertion

Assertions are CHECK constraints that you can apply on multiple tables. Due to this, you can't create assertions while defining a table. Here's the syntax that you must use while creating an assertion:

```sql
CREATE ASSERTION (name of constraint) CHECK (the search conditions)
```

Defining an assertion is similar to defining a table-level CHECK constraint. After typing CHECK, you need to specify the search condition/s.

Let's analyze a new example. Assume that the BOOK_TITLES table has a column that holds the quantity of books in stock. The total for this table should always be lower than your desired inventory. This example uses an assertion to check whether the total of the STOCK_AVAILABILITY column is lower than 3000.

```sql
CREATE ASSERTION LIMIT_STOCK_AVAILABILITY CHECK ( ( SELECT SUM (STOCK_AVAILABILITY) FROM BOOK_TITLES ) < 3000 ) ;
```

This statement uses a subquery (i.e. “SELECT SUM (STOCK_AVAILABILITY) FROM BOOK_TITLES”) and compares it with 3000. The subquery starts with an SQL keyword, SELECT, which queries information from any table. The SQL function called SUM adds up all of the values inside STOCK_AVAILABILITY. The keyword FROM, on the other hand, sets the column that holds the table. The system will then compare the subquery's result to 3000. You will get an error message if you add an entry to the STOCK_AVAILABILITY column that makes the total exceed 3000.

## How to Create a Domain and a Domain Constraint

As mentioned earlier, you may also insert the CHECK constraint into your domain definitions. This kind of constraint is similar to the ones you've seen earlier. The only difference is that you don't attach a domain constraint to a particular table or column. Actually, a domain constraint uses VALUE, another SQL keyword, while referring to a value inside a column specified for that domain. Now, let's discuss the syntax you need to use to generate new domains:

```sql
CREATE DOMAIN (name of domain) {AS} (type of data)
{ DEFAULT (the default value) }
{ CONSTRAINT (name of constraint) } CHECK < (the search condition) >
```

This syntax has elements you've seen before, as you’ve seen default clauses and data types in the third chapter. The definition of the constraint, on the other hand, has some similarities with the ones discussed in the last couple of sections.

In the example below, you will generate an INT-type domain. This domain can only accept values between 1 and 50:

```sql
CREATE DOMAIN BOOK_QUANTITY AS INT CONSTRAINT TS_BOOK_QUANTITY CHECK (VALUE BETWEEN 1 AND 50);
```

This example involves one new item, which is the VALUE keyword. As mentioned earlier, this keyword refers to a column's specified value using the BOOK_QUANTITY domain. Consequently, you will get an error message if you will enter a value that doesn't satisfy the assigned condition (i.e. each value must be between 1 and 50).

format. You'll learn about the third line later.

You need to set the view's name in the first part of the definition. Additionally, you should name the view's columns if you are facing any of the following circumstances:

- If you need to perform an operation to get the column's values, instead of just copying them from a table.
- If you are working with duplicate column names. This situation happens when you combine tables.

You may set names for your columns even if you don't need to. For instance, you may assign logical names to your columns so that even an inexperienced user can understand them.

The second part of the format has a mandatory keyword (i.e. AS) and a placeholder for the query. Despite its apparent simplicity, the query placeholder may involve a complicated structure of SQL statements that perform different operations.

Let's analyze a basic example:

```sql
CREATE VIEW BOOKS_IN_STOCK
( BOOK_TITLE, AUTHOR, STOCK_AVAILABILITY ) AS
SELECT BOOK_TITLE, AUTHOR, STOCK_AVAILABILITY

FROM BOOK_INVENTORY¹²
```

This sample is one of the simplest views that you can create. It gets three columns from a table. Remember that SQL isn't strict when it comes to line breaks and spaces. For instance, while creating a view, you may list the column names (if applicable) on a separate line. Database management systems won't care which coding technique you use. However, you can ensure the readability of your codes by adopting a coding style.

Now, let's dissect the sample code given above. The first part sets BOOKS_IN_STOCK as the view's name. The second part sets the name of the columns and contains the SQL keyword AS.

If you don't specify the names you want to use, the view's columns will just copy the names of the table's columns. The last two lines hold the search expression, which is a SELECT statement. Here it is:

```sql
SELECT BOOK_TITLE, AUTHOR, STOCK_AVAILABILITY
```
