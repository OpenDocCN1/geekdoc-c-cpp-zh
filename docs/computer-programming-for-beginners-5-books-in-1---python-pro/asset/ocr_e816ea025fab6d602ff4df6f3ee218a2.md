the table’s columns. This form is generally used if you need to add data to all columns.

You will use the following syntax for the first form:

```
INSERT INTO table_name
VALUES (‘value1’, ‘value2’, [NULL]);
```

In the second form, you’ll have to include the column names. The values will be assigned based on the order of the columns’ appearance. This form is typically used if you want to add records to specific columns.

Here’s the syntax:

```
INSERT INTO table_name (column1, column2, column3)
VALUES (‘value1’, ‘value2’, ‘value3’);
```

Notice that in both forms, a comma is used to separate the columns and the values. In addition, you have to enclose character/string and date/time data within quotation marks.

Assuming that you have the following record for an employee:

+   - First NameRobert
+   - Last NamePage
+   - PositionClerk
+   - Salary5,000.00
+   - 282 Patterson Avenue Illinois

To insert this data into the EMPLOYEES table, you can use the following statement:

```
INSERT INTO EMPLOYEES (FIRST_NAME, LAST_NAME, POSITION,
SALARY, ADDRESS)
VALUES (‘Robert’, ‘Page’, ‘Clerk’, 5000.00, ‘282 Patterson Avenue, Illinois’);
```

To view the updated table, here’s the syntax:

```
SELECT * FROM table_name;
```

To display the data stored in the EMPLOYEES’ table, use the following statement:

```
SELECT * FROM EMPLOYEES:
```