```
```sql
UPDATE ReminderDb SET dueDate = ? WHERE id = ?;
```
```

+   1. You add a new column called `dueDate` to the table. It can be null, so you don’t add the `NOT NULL` keyword. Since there’s no `Date` type in SQLite, you’ll store the timestamp as `INTEGER`.
+   2. Next, you write an update statement that will let you set a due date on a reminder.

Third, create a file called **1.sqm** in the same directory to write the migration statements. You must always name this file using this pattern: `<version to upgrade from>.sqm`.

```
```sql
ALTER TABLE ReminderDb ADD COLUMN dueDate INTEGER;
```
```

You’re telling the system to alter the `ReminderDb` table and add a new column for `dueDate`.

To check that migration can happen without any errors, run `verifySqlDelightMigration` task from the Gradle pane in Android Studio or in command line.

This will consider **1.db**, **1.sqm** and **Table.sq** to check the validity of the SQL statements you wrote.

![](bbox=[0.321, 0.536, 0.678, 0.819])

*Fig. 10.5 – Verify SqlDelight Migration Gradle Task*

If this test passed successfully, run the `generateCommonMainOrganizeDbScheme` task once again to save the current schema as **2.db**. You can safely check these files out into your git repository as well.