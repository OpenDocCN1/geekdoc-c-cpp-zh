Create a table called Department. The table should have two columns: Department_Id, which should be an integer data type and the primary key. The other column should be Department_Name, which should be a data type of VARCHAR of 30 bytes.

Alter the name of your database from Company to Company_Db.

# Running the DDL Script

Now, it’s time for you to download the following DDL script to create the rest of the tables that you’ll be working with. Don’t worry, I’ve written the script so that it will successfully run by clicking the ‘Execute’ button. Just make sure that you have completed the exercises correctly, otherwise it will not work.

Once you’ve performed this, you’ll start using your knowledge of DML to add and retrieve data.

# Data Manipulation Language (DML)

DML or Data Manipulation Language is exactly what it sounds like; it manipulates the data. The statements that are part of DML allow you to modify existing data, create new data, or even delete data.

Take note that DML is not specific to objects like modifying a table’s structure or a database’s settings, but it works with the data within such objects.

SELECT - This statement is the most common SQL statement, and it allows you to retrieve data. It is also used in many reporting scenarios.

**--Selects two columns from a table**

```
SELECT

Column_Name1,

Column_Name2

FROM Table_Name
```

INSERT - This statement allows you to insert data into the tables of a particular database.

**--Inserts three rows into the table**

```
INSERT INTO Table_Name

(**Column_Name1, Column_Name2) --These two items are the columns**

VALUES
```