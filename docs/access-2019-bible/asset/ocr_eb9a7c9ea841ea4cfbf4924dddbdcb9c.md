# NOTE

Note that the UNION operator effectively performs a SELECT DISTINCT on the resulting data sets. This means that the UNION statement could very well eliminate duplicate rows where all the values in every field are identical between the two data sets. If you find that you’re missing records when running a UNION query, consider using the UNION ALL operator. UNION ALL performs the same function as UNION, except it does not apply the SELECT DISTINCT and thus does not eliminate duplicate rows.

# Creating a table with the CREATE TABLE statement

Often in your analytical processes, you’ll need to create a temporary table in order to group, manipulate, or simply hold data. The CREATE TABLE statement allows you to do just that with one SQL-specific query.

Unlike a make-table query, the CREATE TABLE statement is designed to create only the structure or schema of a table. No records are ever returned with a CREATE TABLE statement. This statement allows you to strategically create an empty table at any point in your analytical process.

The basic syntax for a CREATE TABLE statement is as follows:

```
CREATE TABLE TableName
(<Field1Name> Type(<Field Size>), <Field2Name> Type(<Field Size>))
```

To use the CREATE TABLE statement, simply start a new query, switch to SQL view, and define the structure for your table.

In the following example, a new table called TempLog is created with three fields. The first field is a Text field that can accept 50 characters, the second field is a Text field that can accept 255 characters, and the third field is a Date field:

```
CREATE TABLE TempLog
([User] Text(50), [Description] Text, [LogDate] Date)
```

# NOTE

Notice that in the preceding example, no field size is specified for the second text column. If the field size is omitted, Access will use the default field size specified for the database.

# Manipulating columns with the ALTER TABLE statement

The ALTER TABLE statement provides some additional methods of altering the structure of a table behind the scenes. There are several clauses you can use with the ALTER TABLE statement, four of which are quite useful in Access data analysis: ADD, ALTER COLUMN, DROP COLUMN, and ADD CONSTRAINT.