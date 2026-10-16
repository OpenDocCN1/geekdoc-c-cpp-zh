Suppose that the CUSTOMERS table contains one or more missing values in the CUSTCITY column. If you tried to add a NOT NULL constraint, it would be rejected. You can successfully apply the NOT NULL constraint only when missing values are reclassified or recoded.

# SQL Code

```
PROC SQL;
    ALTER TABLE CUSTOMERS
        ADD CONSTRAINT NOT_NULL_CUSTCITY NOT NULL(CUSTCITY);
QUIT;
```

The SAS log shows that the NOT NULL constraint cannot be defined in an existing table when a column’s data contains one or more missing values. The violation produces an error message that results in the rejection of the constraint.

# SAS Log Results

```
PROC SQL;
    ALTER TABLE CUSTOMERS
        ADD CONSTRAINT NOT_NULL_CUSTCITY NOT NULL(CUSTCITY);
ERROR: Integrity constraint NOT_NULL_CUSTCITY was rejected because 1 observations failed the constraint.
QUIT;
NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE SQL used:
      real time          0.01 seconds
      cpu time           0.00 seconds
```

# Enforcing Unique Values with a UNIQUE Constraint

A UNIQUE constraint prevents duplicate values from propagating in a table. If you use a CREATE TABLE statement, then you can apply a UNIQUE constraint to any column where duplicate data is not desired. Suppose that you want to avoid the propagation of duplicate values in the CUSTNUM (Customer Number) column in a new table called CUSTOMER_CITY. By specifying the UNIQUE constraint for the CUSTNUM column with the CREATE TABLE statement, you prevent duplicate values from populating the table.

# SQL Code

```
PROC SQL;
    CREATE TABLE CUSTOMER_CITY
        (CUSTNUM NUM UNIQUE,
         CUSTCITY CHAR(20));
QUIT;
```

When you define a UNIQUE constraint and attempt to populate a table with duplicate data values, the rows will be rejected and the table will be restored to its original state prior to the add operation taking place. Essentially, the insert fails because the UNIQUE constraint prevents any duplicate values for a defined column from populating the table. In the next example, several rows of data