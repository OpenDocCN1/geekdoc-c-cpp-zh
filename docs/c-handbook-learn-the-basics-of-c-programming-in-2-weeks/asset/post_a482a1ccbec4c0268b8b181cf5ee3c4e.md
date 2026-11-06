
## The INSERT INTO Command

```
INSERT INTO table_name( column1, column2....columnN)
VALUES ( value1, value2....valueN);
```

## The UPDATE Command

```
UPDATE table_name
SET column1 = value1, column2 = value2....columnN=valueN
[ WHERE  CONDITION ];
```

## The DELETE Command

```
DELETE FROM table_name
WHERE {CONDITION};
```

## The CREATE DATABASE Command

```
CREATE DATABASE database_name;
```

## The DROP Database Command

```
DROP DATABASE database_name;
```

## The USE Command

```
USE DATABASE database_name;
```

## The COMMIT Command

```
COMMIT;
```

## The ROLLBACK Command

```
ROLLBACK;
```

## Chapter 4: The Different Data Types in SQL

In the SQL language, data type is a characteristic that determines the type of any database object. All columns, variables, and expressions involve data types in SQL.

You should indicate data types while generating new tables. Additionally, you have to select data types for your tables based on your needs.

This computer language supports many types of data. Let's divide these types into six major categories:

- 1. **Exact Numeric**

| DATA TYPE | FROM | TO |
|---|---:|---:|
| Bigint | -9,223,372,036,854,775,808 | 9,223,372,036,854,775,807 |
| Int | -2,147,483,648 | 2,147,483,647 |
| Smallint | -32,768 | 32,767 |
| Tinyint | 0 | 255 |
| Bit | 0 | 1 |
| Decimal | -10^38 + 1 | 10^38 - 1 |
| Numeric | -10^38 + 1 | 10^38 - 1 |
| Money | -922,337,203,685,477.5808 | +922,337,203,685,477.5807 |
| Smallmoney | -214,748.3648 | +214,748.3647 |

- 2. **Approximate Numeric**

| DATA TYPE | FROM | TO |
|---|---:|---:|
| Float | -1.79E + 308 | 1.79E + 308 |
| Real | -3.40E + 38 | 3.40E + 38 |

- 3. **Time and Date**

| DATA TYPE | FROM | TO |
|---|---|---|
| Datetime | Jan 1, 1753 | Dec 31, 9999 |
| Smalldatetime | Jan 1, 1900 | Jun 6, 2079 |
| Date | Stores a date like June 30, 1991 | |
| Time | Stores a time of day like 12:30 P.M. | |

- 4. **Character Strings – This is divided into two subcategories:**

### 1. Unicode Strings

| DATA TYPE | Description |
|---|---|
| Nchar | Maximum length of 4,000 characters. ( Fixed length Unicode) |
| Nvarchar | Maximum length of 4,000 characters. (Variable length Unicode) |
| nvarchar(max) | Maximum length of 2^31 characters (SQL Server 2005 only). ( Variable length Unicode) |
| Ntext | Maximum length of 1,073,741,823 characters. ( Variable length Unicode ) |

### 2. Non-Unicode Strings

| DATA TYPE | FROM | TO |
|---|---|---|
| Char | Char | Maximum length of 8,000 characters. ( Fixed length non-Unicode characters) |
| Varchar | Varchar | Maximum of 8,000 characters. (Variable-length non-Unicode data). |
| varchar(max) | varchar(max) | Maximum length of 2^31 characters, Variable-length non-Unicode data (SQL Server 2005 only). |
| Text | text | Variable-length non-Unicode data with a maximum length of 2,147,483,647 characters. |

### 5. Binary

| DATA TYPE | Description |
|---|---|
| Binary | Maximum length of 8,000 bytes.(Fixed-length binary data ) |
| Varbinary | Maximum length of 8,000 bytes. (Variable length binary data) |
| varbinary(max) | Maximum length of 2^31 bytes (SQL Server 2005 only). ( Variable length Binary data) |
| Image | Maximum length of 2,147,483,647 bytes. ( Variable length Binary Data) |

### 6. Miscellaneous

This category involves the following data types:

- timestamp – This data type stores a unique number that becomes updated whenever a row becomes updated. You may access this unique number in any part of your database.
- xml – This data type stores XML (i.e. Extensible Markup Language) information. You may save XML data in columns or variables.
- table – This type saves the results of your database queries so that you can use

## Chapter 5: The Operators in the SQL Language

Operators are reserved words or characters that you can use for your SQL commands. Generally, operators are used in the WHERE section of your commands to conduct operations (e.g. comparisons, mathematical operations, etc.).

You can use an operator to specify a condition in your SQL statements. In some cases, you may utilize an operator as a conjunction if your commands involve multiple conditions.

This chapter will discuss the four types of operators supported by SQL:

- Logical Operators
- Arithmetic Operators
- Comparison Operators
- Operators that can nullify conditions

### The Logical Operators

These are the logical operators that you can use in the SQL computer language:

- IN – You can use this operator to compare a value against your specified literal values.
- OR – This operator combines various conditions in the WHERE section of your SQL commands.
- AND – This operator allows you to include multiple conditions in the WHERE clause of your SQL commands.
- ALL – This operator compares a value against values that are inside a different value set.
- ANY – This operator uses a condition to perform comparisons.
- LIKE – This operator uses wildcard operators to compare values against similar ones.

- UNIQUE – This operator checks the uniqueness of your entries. To accomplish this, the UNIQUE operator scans the entire table and searches for redundant data.
- EXISTS – This operator searches for rows that meet specified criteria.
- BETWEEN – This operator searches for values that are inside a certain range. When using BETWEEN, you should indicate the highest value and the lowest value.
- IS NULL – This operator compares a value against a NULL value.

### The Arithmetic Operators

To help you understand these operators, let's use two sample variables: x = 1; y = 2.

- “ + ” – You should use this operator to perform addition. For instance, x + y = 3.
- “ - ” – You must use this operator to perform subtraction. It will subtract the value of the right operand from that of the left operand. For example, y – x = 1.
- “ * ” – You should use this operator when performing multiplication. Here's an example: x * y = 2.
- “ / ” – You should use this operator when performing division. For example: y / x = 2.

### The Comparison Operators

Let's assume that x = 2 and y = 4.

- “ = ” – This operator checks the equality of two values. If the values are equal, the condition is true. For example: (x = y) is not true.
- “ != ” – This operator checks the equality of two values. If the values are unequal, the condition is true. For example: (y != x) is true.
- “ <> ” – This operator is the same as “ != ” . For example: (x <> y) is true.
- “ > ” – This operator checks if the left operand ’ s value is greater than that of the right operand. If it is, the condition is true. For instance: (y > x) is true.
- “ < ” – This operator checks whether the left operand ’ s value is less than that of the right operand. If it is, the condition is true. For instance: (x < y) is true.
- “ >= ” – This operator checks if the left operand ’ s value is greater than or equal to that of the right operand. If it is, the condition is true. For example: (y >= x) is true.
- “ <= ” – This operator checks if the left operand ’ s value is lesser than or equal to that of the right operand. If it is, the condition is true. For instance: (x <= y) is true.

### The Operator that can Nullify Conditions

- NOT – This operator can reverse the function of the logical operator you ’ ll use it with. For example: NOT IN, NOT EXISTS, NOT BETWEEN, etc.

## Chapter 6: The SQL Expressions

Basically, an expression is a group of values, functions, and operators. SQL expressions can help you evaluate database values.

In this computer language, an expression is a formula that you must write using a query language. You may also use an expression to run a database query for certain pieces of information.

### The Syntax

Here is the format of the SELECT command:

```sql
SELECT column1, column2, columnN
FROM table_name
WHERE [CONDITION EXPRESSION];
```

Now, let's talk about the expressions supported by SQL:

*The Boolean Expressions* — These expressions retrieve data by matching a single value.
Here is the basic syntax of a Boolean expression:

```sql
SELECT column1, column2, columnN
FROM table_name
WHERE SINGLE VALUE MATCHING EXPRESSION;
```

*The Numeric Expressions* — You can use these expressions to conduct mathematical operations in your database queries. Here is the syntax that you should use:

```sql
SELECT numerical expression as OPERATION NAME
[FROM table_name
WHERE CONDITION] ;
```

The Date Expressions — These expressions give you the time and date information of your system.
