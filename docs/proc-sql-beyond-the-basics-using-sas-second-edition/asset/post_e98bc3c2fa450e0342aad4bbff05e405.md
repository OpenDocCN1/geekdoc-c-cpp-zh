
with a defined UNIQUE constraint are prevented from being populated in the CUSTOMER_CITY table because one row contains a duplicate CUSTNUM value.

### SQL Code

```
PROC SQL;
    INSERT INTO CUSTOMER_CITY
    VALUES (101,'La Mesa Computer Land')
    VALUES (1301,'Spring Valley Byte Center')
    VALUES (1301,'Chula Vista Networks');
QUIT;
```

The SAS log shows that the UNIQUE constraint prevented the three rows of data from being populated in the CUSTOMER_CITY table. The violation caused an error message that resulted in the failure of the add/update operation.

### SAS Log Results

```
PROC SQL;
    INSERT INTO CUSTOMER_CITY
    VALUES (101,'La Mesa Computer Land')
    VALUES (1301,'Spring Valley Byte Center')
    VALUES (1301,'Chula Vista Networks');
ERROR: Add/Update failed for data set WORK.CUSTOMER_CITY because data value(s) do not comply with integrity constraint _UNO001_.
NOTE: This insert failed while attempting to add data from VALUES clause 3 to the data set.
NOTE: Deleting the successful inserts before error noted above to restore table to a consistent state.
QUIT;
NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE SQL used:
    real time          1.12 seconds
    cpu time           0.06 seconds
```

## Validating Column Values with a CHECK Constraint

A CHECK constraint validates data values against a list of values, minimum and maximum values, as well as a range of values before populating a table. Using either a CREATE TABLE or ALTER TABLE statement, you can apply a CHECK constraint to any column that requires data validation to be performed. In the next example, suppose you want to validate data values in the PRODTYPE (Product Type) column in the PRODUCTS table. When you specify a CHECK constraint against the PRODTYPE column using the ALTER TABLE statement, product type values will first need to match the list of defined values or the rows will be rejected.

### SQL Code

```
PROC SQL;
    ALTER TABLE PRODUCTS
        ADD CONSTRAINT CHECK_PRODUCT_TYPE
        CHECK (PRODTYPE IN ('Laptop',
            'Phone',
            'Software',
            'Workstation'));
QUIT;
```

With a CHECK constraint defined, each row must meet the validation rules that are specified for the column before the table is populated. If any row does not pass the validation checks based on the established validation rules, then the add/update operation fails and the table is automatically restored to its original state prior to the operation taking place. In the next example, three rows of data are validated against the defined CHECK constraint established for the PRODTYPE column.

### SQL Code

```
PROC SQL;
    INSERT INTO PRODUCTS
        VALUES (5005,'Internet Software',500,'Software',99.)
        VALUES (1701,'Elite Laptop',170,'Laptop',3900.)
        VALUES (2103,'Digital Cell Phone',210,'Fone',199.);
QUIT;
```

The SAS log displays the results after attempting to add the three rows of data. Because one row violates the CHECK constraint with a value of “Fone”, the rows are not added to the PRODUCTS table. The violation produces an error message that results in the failure of the add/update operation.

### SAS Log Results

```
PROC SQL;
    INSERT INTO PRODUCTS
        VALUES (5005,'Internet Software',500,'Software',99.)
        VALUES (1701,'Elite Laptop',170,'Laptop',3900.)
        VALUES (2103,'Digital Cell Phone',210,'Fone',199.);
ERROR: Add/Update failed for data set WORK.PRODUCTS because data value(s) do not comply with integrity constraint CHECK_PRODUCT_TYPE.
NOTE: This insert failed while attempting to add data from VALUES clause 3 to the data set.
NOTE: Deleting the successful inserts before error noted above to restore table to a consistent state.
QUIT;
NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE SQL used:
    real time          0.09 seconds
    cpu time           0.02 seconds
```

## Referential Integrity Constraints

The second type of constraint that is available in the SQL procedure is referred to as a referential integrity constraint. Enforced through primary and foreign keys between two or more tables, referential integrity constraints are built into a database environment to prevent data integrity issues from occurring. Specific types of referential integrity constraints and constraint action clauses are used to enforce update and delete operations and consist of the following:

### Referential Integrity Constraints

- Primary key
- Foreign key

### Referential Integrity Constraint Action Clauses

- RESTRICT (Default)
- SET NULL
- CASCADE

The action clauses are discussed in the “Establishing a Foreign Key” section in this chapter.

### Establishing a Primary Key

A primary key consists of one or more columns with a unique value that is used to identify individual rows in a table. Depending on the nature of the columns used, a single column may be all that is necessary to identify specific rows. In other cases, two or more columns may be needed to adequately identify a row in a referenced table. Suppose that you need to uniquely identify specific rows in the MANUFACTURERS table. By establishing the Manufacturer Number (MANUNUM) as the unique identifier for rows, a key is established. The next example specifies the ALTER TABLE statement to create a primary key using MANUNUM in the MANUFACTURERS table.

### SQL Code

```
PROC SQL;
  ALTER TABLE MANUFACTURERS
    ADD CONSTRAINT PRIM_KEY PRIMARY KEY (MANUNUM);
QUIT;
```

The SAS log shows that the MANUFACTURERS table has been modified successfully after creating a primary key using the MANUNUM column.

### SAS Log Results

```
PROC SQL;
  ALTER TABLE MANUFACTURERS
    ADD CONSTRAINT PRIM_KEY PRIMARY KEY (MANUNUM);
NOTE: Table WORK.MANUFACTURERS has been modified, with 4 columns.
QUIT;
NOTE: PROCEDURE SQL used:
  real time          0.07 seconds
  cpu time           0.01 seconds
```

Suppose that you also need to uniquely identify specific rows in the PRODUCTS table. By specifying PRODNUM (Product Number) as the primary key, the next example specifies the ALTER TABLE statement to create the unique identifier for rows in the table.

### SQL Code

```
PROC SQL;
    ALTER TABLE PRODUCTS
        ADD CONSTRAINT PRIM_PRODUCT_KEY PRIMARY KEY (PRODNUM);
QUIT;
```

The SAS log shows that the PRODUCTS table has been modified successfully after establishing a primary key using the PRODNUM column.

### SAS Log Results

```
PROC SQL;
    ALTER TABLE PRODUCTS
        ADD CONSTRAINT PRIM_PRODUCT_KEY PRIMARY KEY (PRODNUM);
NOTE: Table WORK.PRODUCTS has been modified, with 5 columns.
    QUIT;
NOTE: PROCEDURE SQL used:
        real time           0.03 seconds
        cpu time            0.01 seconds
```

### Establishing a Foreign Key

A foreign key consists of one or more columns in a table that references or relates to values in another table. The column(s) that is used as a foreign key must match the column(s) in the table that is referenced. The purpose of a foreign key is to ensure that rows of data in one table exist in another table thereby preventing the possibility of lost or missing linkages between tables. The enforcement of referential integrity rules has a positive and direct effect on data reliability issues.

Suppose that you want to ensure that data values in the INVENTORY table have corresponding and matching data values in the PRODUCTS table. By establishing PRODNUM (Product Number) as a foreign key in the INVENTORY table, you ensure a strong level of data integrity between the two tables. This essentially verifies that key data in the INVENTORY table exists in the PRODUCTS table. In the next example, a foreign key is created using the PRODNUM column in the INVENTORY table by specifying the ALTER TABLE statement.

### SQL Code

```
PROC SQL;
    ALTER TABLE INVENTORY
        ADD CONSTRAINT FOREIGN_PRODUCT_KEY FOREIGN KEY (PRODNUM)
            REFERENCES PRODUCTS
                ON DELETE RESTRICT
                ON UPDATE RESTRICT;
QUIT;
```
