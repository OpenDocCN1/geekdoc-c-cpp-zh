
![](img/239ff1e8a63502805c86c4dfbd71509a_249_0.png)

We can now combine the query with the DISTINCT keyword and see what the query returns:

```sql
Select * From Student
where StudentAge >
(Select StudentAge from Student
where StudName = 'Stacy'
)
```

Notice that in Query 1, we’ve used round brackets to append a sub-query in the “where” clause. The above query will retrieve the records of all students from the “Student” table where the age of the student is greater than the age of “Stacy”. The age of “Stacy” is 20; therefore, in the output, you shall see the records of all students aged greater than 20. The output is the following:

| StudID | StudName | StudentAge | StudentGender | DepID |
|--------|----------|-----------:|---------------|-------|
| 1 | Alice | 21 | Male | 2 |
| 4 | Jacobs | 22 | Male | 5 |
| 6 | Shane | 22 | Male | 4 |
| 7 | Linda | 24 | Female | 4 |
| 9 | Wolfred | 21 | Male | 2 |
| 10 | Sandy | 25 | Female | 1 |
| 14 | Mark | 23 | Male | 5 |
| 15 | Fred | 25 | Male | 2 |
| 16 | Vic | 25 | Male | NULL |
| 17 | Nick | 25 | Male | NULL |

Similarly, if you want to update the name of all the students with department name “English”, you can do so using the following sub-query:

### Query 2

```sql
Update Student
Set StudName = StudName + ' Eng'
where Student.StudID in (
Select StudID
from Student
Join Department
On Student.DepID = Department.DepID
where DepName = 'English'
)
```

In the above query, the student IDs of all the students in the English department have been retrieved using a JOIN statement in the sub-query. Then, using an UPDATE statement, the names of all those students have been updated by appending the string “Eng” at the end of their names. A WHERE statement has been used to match the student IDs retrieved by using a sub-query.

Now, if you display the Student’s name along with their Department name, you will see “Eng” appended to the names of the students that belong to the English department.

## Exercise 9

### Task

Delete the records of all students from the “Student” table where student’s IDs are less than the ID of “Linda”.

### Solution

```sql
Delete From Student
where StudID <
(Select StudID from Student
where StudName = 'Linda'
)
```

## SQL Character Functions

SQL character functions are used to modify the appearance of retrieved data. Character functions do not modify the actual data, but rather perform certain modifications in the way data is represented. SQL character functions operate on string type data. In this chapter, we will look at some of the most commonly used SQL character functions.

### Note

- **Concatenation (+)**

  Concatenation functions are used to concatenate two or more strings. To concatenate two strings in SQL, the ‘+’ operator is used. For example, we can join student names and student genders from the student column and display them in one column, like the following:

  ```sql
  Select StudName +' '+StudentGender as NameAndGender
  from Student
  ```

- **Replace**

  The replace function is used to replace characters in the output string. For instance, the following query replaces “ac” with “rs” in all student names.

  ```sql
  Select StudName, REPLACE(StudName, 'ac', 'rs') as ModifiedColumn
  From Student
  ```

  The first parameter in the replace function is the column whose value you want to replace; the second parameter is the character sequence which you want to replace, followed by the third parameter which denotes the character sequence you want to insert in place of the old sequence.

- **Substring**

  The substring function returns the specified number of characters starting from the specified position. The following query displays the first three characters of student names.

  ```sql
  Select StudName, substring(StudName, 1, 3) as SubstringColumn
  From Student
  ```

- **Length**

  The length function is used to get the length of values of a particular column. For instance, to get the length of names of students in the “Student” table, the following query can be executed:

  ```sql
  Select StudName, Len(StudName) as NameLength
  from Student
  ```

  Note that in the above query, we used the Len() function to get the length of the names; this is because in the SQL server, the Len() function is used to calculate the length of any string.

- **IFNULL**

  The IFNULL function checks if there is a Null value in a particular Table column. If a NULL value exists, it is replaced by the value passed as the second parameter to the IFNULL function. For instance, the following query will display 50 as the department ID of the students with a null department ID.

  ```sql
  Select Student.DepID, IFNULL(Student.DepID, 50)
  from Student
  ```

- **LTRIM**

  The LTRIM function trims all the leading empty spaces from the values in the column specified as parameters to the LTRIM function. For instance, if you want to remove all the empty spaces before the names of the students in the “Student” table, you can use the LTRIM query, like the following:

  ```sql
  Select Student.StudName, LTRIM(Student.StudName)
  from Student
  ```

- **RTRIM**

  The RTRIM function trims all the trailing empty spaces from the values in the column specified as parameters to the RTRIM function. For instance, if you want to remove all the empty spaces that come after the names of the students in the “Student” table, you can use the RTRIM query, like the following:

  ```sql
  Select Student.StudName, RTRIM(Student.StudName)
  from Student
  ```

## SQL Constraints

Constraints refer to rules that are applied on the columns of database tables. They help us impose restrictions on the kind of data that can be kept in that table. This way, we can ensure that there is reliability and accuracy of the data in the database.

Constraints can be imposed at column level or at the table level. The column constraints can only be imposed on a single column, while the table level constraints are applied to the entire table.

### NOT NULL Constraint

The default setting in SQL is that a column may hold null values. If you don’t want to have a column without a value, you can specify this constraint.

Note that NULL means unknown data rather than no data. This constraint can be defined when you are creating a table. Let’s demonstrate this by creating a sample table:

```sql
CREATE TABLE MANAGERS(
    ID   INT NOT NULL,
    NAME VARCHAR (15) NOT NULL,
    DEPT VARCHAR(20)  NOT NULL,
    SALARY  DECIMAL (20, 2),
    PRIMARY KEY (ID)
);
```

Above, we have created a table named MANAGERS with 4 columns, and the NOT NULL constraint has been imposed on three of these columns. This means that you must specify a value for each of these columns with the constraint; otherwise, an error will be raised.

Note that we did not impose the NOT NULL constraint to the SALARY column of our table. It is possible for us to impose the constraint on the column even though it has already been created.

```sql
ALTER TABLE MANAGERS
    MODIFY SALARY DECIMAL (20, 2) NOT NULL;
```

```text
mysql> ALTER TABLE MANAGERS
    -> MODIFY SALARY DECIMAL (20, 2) NOT NULL;
Query OK, 0 rows affected (0.23 sec)
Records: 0 Duplicates: 0 Warnings: 0

mysql>
```

Now, the column cannot accept a null value.

### Default Constraint

This constraint will provide a default value to the column if a value for the column is not specified in the INSERT INTO statement.

Consider the example given below:

```sql
CREATE TABLE SUPPLIERS(
    ID INT NOT NULL,
    NAME VARCHAR (15) NOT NULL,
    ADDRESS CHAR (20),
    ARREARS DECIMAL (16, 2) DEFAULT 6000.00,
    PRIMARY KEY (ID)
);
```

Suppose you had already created the table but you needed to add a default constraint on the ARREARS column. You can do it like this:

```sql
ALTER TABLE SUPPLIERS
MODIFY ARREARS DECIMAL (16, 2) DEFAULT 6000.00;
```

This will update the table, and a default constraint will be created for the column.

If you no longer need this default constraint to be in place, you can drop it by running the command given below:

```sql
ALTER TABLE SUPPLIERS
```
