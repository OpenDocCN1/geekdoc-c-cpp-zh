
```sql
('Value1', 1), -- Here, I'm inserting Value1 into Column_Name1 and the number 1 in Column_Name2.
('Value2', 2),
('Value3', 3)
```

Now, it is time to insert data into your Department table. Insert the values as shown below. For example, the Department Name of Marketing must have a Department ID of 1, and so on.

- Department_Id: 1, Department_Name: Marketing
- Department_Id: 2, Department_Name: Development
- Department_Id: 3, Department_Name: Sales
- Department_Id: 4, Department_Name: Human Resources
- Department_Id: 5, Department_Name: Customer Support
- Department_Id: 6, Department_Name: Project Management
- Department_Id: 7, Department_Name: Information Technology
- Department_Id: 8, Department_Name: Finance/Payroll
- Department_Id: 9, Department_Name: Research and Development

UPDATE - Allows you to update existing data. For instance, you may change an existing piece of data in a table to another value.

It’s recommended to use caution when updating values in a table. You could give all rows within one column the same value if you don’t specify a condition in the WHERE clause.

```sql
-- Updating a value or set of values in one column of a table
UPDATE Table_Name
SET
    Column_Name1 = 'New Value 1', -- Specify what your new value should be here
    Column_Name2 = 'New Value 2'
WHERE
    Column_Name1 = 'Old Value' -- Using the WHERE clause as a condition

-- Updates all rows in the table with the same value for one specific column
UPDATE Table_Name
SET Column_Name1 = 'Value'⁴⁹
```

Now, you will update one of the department names in your table. Let’s say that you feel like the name ‘Finance/Payroll’ won’t work because payroll is handled by employees via an online web portal. So, that leaves finance, but it’s best to call this department ‘Accounting’ instead, due to the responsibilities of those in the department.

Update the Department table and change the value from ‘Finance/Payroll’ to ‘Accounting’ based on its ID.

DELETE - This action is self-explanatory; it deletes data from a specified object, like a table. It’s best to use caution when running the DELETE statement.

If you don’t use the WHERE clause in your query, you’ll end up deleting all of the data within the table. So, it’s always best to use a WHERE clause in a DELETE statement.

*Note: Much like the UPDATE statement, you can also swap out DELETE with SELECT in your statement to see what data you will be deleting, as long as you’re using the WHERE clause in your query. Like the UPDATE statement, when you delete one value, it’s best to use the primary key as a condition in your WHERE clause!*

```sql
-- Uses a condition in the DELETE statement to only delete a certain value or set of values
DELETE FROM Table_Name
WHERE Column_Name1 = 'Some Value'

-- Deletes all of the data within a table since the WHERE clause isn't used
DELETE FROM Table_Name
```

Let’s say that this company doesn’t actually have a Research and Development (R&D) department. Perhaps they haven’t grown enough yet or don’t require that department.

For this exercise, delete the ‘Research and Development’ department from the Department table based on its ID.

### Running the DML Script

Now, it’s time for you to download the following DML script in order to populate the Company_Db database with data. Again, make sure that you have completed the exercises correctly, otherwise it will not work.

This data will be used in the following exercises in the ‘Transforming Data’ section. So, please keep in mind that each exercise refers to the Company_Db database, unless specified otherwise.

## CHAPTER 6: Database Administration

> “Laws too gentle are seldom obeyed; too severe, seldom executed.” – Benjamin Franklin

In order to start on the path of a Database Administrator, Database Developer or even a Data Analyst, you’ll need to know how to back up, restore and administer databases. These are essential components to maintaining a database and are definitely important responsibilities.

### Recovery Models

There are several different recovery models that can be used for each database in the SQL Server. A recovery model is an option or model for the database that determines the type of information that can be backed up and restored.

Depending on your situation, like if you cannot afford to lose critical data or you want to mirror a Production environment, you can set the recovery model to what you need. Also, keep in mind that the recovery model that you choose could also affect the time it takes to back up or restore the database and logs, depending on their size.

Below are the recovery models and a brief explanation of each. The SQL statement example at the end of each is what you would use in order to set the recovery model.

#### Full

This model covers all of the data within the database, as well as the transaction log history.

When using this model and performing a restore of the database, it offers “point in time” recovery. This means that if there was a point where data was lost from the database during a restore for example, it allows you to roll back and recover that data.

This is the desired recovery model if you cannot afford to lose any data.

It may take more time to back up and restore, depending on the size of the data.

- Can perform full, differential and transaction log backups.

```sql
ALTER DATABASE DatabaseName SET RECOVERY FULL
```

#### Simple

This model covers all of the data within the database too, but recycles the transaction log. When the database is restored, the transaction log will be empty and will log new activity moving forward.

Unlike the “Full” recovery model, the transaction log will be reused for new transactions and therefore cannot be rolled back to recover data if it has accidentally been lost or deleted.

It’s a great option if you have a blank server and need to restore a database fairly quickly and easily, or to just mirror another environment and use it as a test instance.

- Can perform full and differential backups only, since the transaction log is recycled per this recovery model.

```sql
ALTER DATABASE DatabaseName SET RECOVERY SIMPLE
```

#### Bulk Logged

This particular model works by forgoing the bulk operations in SQL Server, like BULK INSERT, SELECT INTO, etc. and does not store these in the transaction logs. This will help free up your transaction logs and make it easier and quicker during the backup and restore process.

Using this method, you have the ability to use “point in time” recovery, as it works much like the “Full” recovery model.

If your data is critical to you and your database processes often use bulk statements, this recovery model is ideal. However, if your database does not often use bulk statements, the “Full” recovery model is recommended.

- Can perform full, differential and transaction log backups.

```sql
ALTER DATABASE DatabaseName SET RECOVERY BULK_LOGGED
```

Let’s say you’re in the middle of a large database project and need to back up the database. Use SQL syntax (and the examples above) to set the recovery model for Company_Db to “Full” to prepare for the backup process.

### Database Backup Methods

There are a few main backup methods that can be used to back up databases in SQL Server, and each one is dependent on the recovery model being used. In the previous section regarding recovery models, the last bullet point in each model discussed the types of backups that can be performed, i.e. full, differential and transaction log.

**Note:** *if you don’t remember the types of backups that can be performed for each recovery model, just give yourself time! Eventually, you will remember them!*

Each backup method will perform the following action:

#### Full:

Backs up the database in its entirety, as well as the transaction log (if applicable.)

Ideal if the same database needs to be added to a new server for testing.

It may take a longer period of time to back up if the database is large in size, in addition to it backing up the entire database and transaction log.

- However, this doesn’t need to be performed nearly as often as a differential since you’re backing up the entire database.

```sql
BACKUP DATABASE DatabaseName TO DISK = 'C:\SQLBackups\DatabaseName.BAK'
```

#### Differential:

It is dependent upon a full back up, so the full backup must be performed first. However, this will back up any data changes between the last full back up and the time that the differential backup takes place.

It is ideal in any situation, but must be done more frequently since there is new data being added to the database frequently.

It is much faster to back up than a full backup and takes up less storage space.

- However, this doesn’t capture the database entirely, so this is the reason it must be performed periodically.

```sql
BACKUP DATABASE DatabaseName TO DISK = 'C:\SQLBackups\DatabaseName.BAK' WITH DIFFERENTIAL
```

#### Transaction Log:
