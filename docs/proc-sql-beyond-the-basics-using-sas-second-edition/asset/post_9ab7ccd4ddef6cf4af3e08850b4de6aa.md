
The SAS log displays the successful creation of the PRODNUM column as a foreign key in the INVENTORY table. By specifying the default values ON DELETE RESTRICT and ON UPDATE RESTRICT clauses, you restrict the ability to change the values of primary key data when matching values are found in the foreign key. The execution of any SQL statement that could violate these referential integrity rules is prevented during SQL processing.

## SAS Log Results

```
PROC SQL;
    ALTER TABLE INVENTORY
    ADD CONSTRAINT FOREIGN_PRODUCT_KEY FOREIGN KEY (PRODNUM)
        REFERENCES PRODUCTS
        ON DELETE RESTRICT
        ON UPDATE RESTRICT;
NOTE: Table WORK.INVENTORY has been modified, with 5 columns.
    QUIT;
NOTE: PROCEDURE SQL used:
      real time           0.01 seconds
      cpu time            0.01 seconds
```

Suppose that a product of a particular manufacturer is no longer available and has been taken off the market. To handle this type of situation, data values in the INVENTORY table should be set to missing once the product is deleted from the PRODUCTS table. The next example establishes a foreign key using the PRODNUM column in the INVENTORY table and sets values to null with the ON DELETE clause.

## SQL Code

```
PROC SQL;
    ALTER TABLE INVENTORY
    ADD CONSTRAINT FOREIGN_MISSING_PRODUCT_KEY FOREIGN KEY (PRODNUM)
        REFERENCES PRODUCTS
        ON DELETE SET NULL;
QUIT;
```

The SAS log displays the successful creation of the PRODNUM column as a foreign key in the INVENTORY table as well as the effect of the ON DELETE SET NULL clause. Specifying this clause will change foreign key values to missing or null for all of the rows with matching values found in the primary key. The execution of any SQL statement that could violate these referential integrity rules is prevented during SQL processing.

## SAS Log Results

```
PROC SQL;
    ALTER TABLE INVENTORY
    ADD CONSTRAINT FOREIGN_MISSING_PRODUCT_KEY FOREIGN KEY (PRODNUM)
        REFERENCES PRODUCTS
        ON DELETE SET NULL;
NOTE: Table WORK.INVENTORY has been modified, with 5 columns.
    QUIT;
NOTE: PROCEDURE SQL used:
    real time          0.02 seconds
    cpu time           0.02 seconds
```

Suppose that you want to ensure that changes to key values in the PRODUCTS table automatically flow over or cascade through to rows in the INVENTORY table. This is accomplished by first creating PRODNUM (Product Number) as a foreign key in the INVENTORY table using the ADD CONSTRAINT clause and referencing the PRODUCTS table. You then specify the ON UPDATE CASCADE clause to enable any changes that are made to the PRODUCTS table to be automatically cascaded through to the INVENTORY table. This ensures that changes to the product number values in the PRODUCTS table automatically occur in the INVENTORY table as well.

## SQL Code

```
PROC SQL;
    ALTER TABLE INVENTORY
    ADD CONSTRAINT FOREIGN_PRODUCT_KEY FOREIGN KEY (PRODNUM)
        REFERENCES PRODUCTS
        ON UPDATE CASCADE
        ON DELETE RESTRICT  /* DEFAULT VALUE */;
QUIT;
```

The SAS log displays the successful creation of the PRODNUM column as a foreign key in the INVENTORY table. When the ON UPDATE and ON DELETE clauses are specified, the execution of any SQL statement that could violate referential integrity rules is strictly prohibited.

## SAS Log Results

```
PROC SQL;
ALTER TABLE INVENTORY
ADD CONSTRAINT FOREIGN_PRODUCT_KEY FOREIGN KEY (PRODNUM)
REFERENCES PRODUCTS
ON UPDATE CASCADE
ON DELETE RESTRICT  /* DEFAULT VALUE */;
NOTE: Table WORK.INVENTORY has been modified, with 5 columns.
QUIT;
NOTE: PROCEDURE SQL used:
real time          0.06 seconds
cpu time           0.01 seconds
```

## Constraints and Change Control

To preserve change control, SAS prohibits changes or modifications to a table that contains a defined referential integrity constraint. When you attempt to delete, rename, or replace a table that contains a referential integrity constraint, an error message is generated and processing stops. The next example illustrates a table copy operation that is performed against a table that contains a referential integrity constraint that generates an error message and stops processing.

## SAS Log Results

```
PROC COPY IN=SQLBOOK OUT=WORK;
SELECT INVENTORY;
RUN;

NOTE: Copying SQLBOOK.INVENTORY to WORK.INVENTORY (memtype=DATA).
ERROR: A rename/delete/replace attempt is not allowed for a data set involved in a referential integrity constraint. WORK.INVENTORY.DATA
ERROR: File WORK.INVENTORY.DATA has not been saved because copy could not be completed.
NOTE: Statements not processed because of errors noted above.
NOTE: PROCEDURE COPY used:
real time          0.44 seconds
cpu time           0.02 seconds
NOTE: The SAS System stopped processing this step because of errors.
```

## Displaying Integrity Constraints

Using the DESCRIBE TABLE statement, the SQL procedure displays integrity constraints along with the table description in the SAS log. The ability to capture this type of information assists with the documentation process by describing the names and types of integrity constraints as well as the contributing columns that they reference.

## SQL Code

```
PROC SQL;
DESCRIBE TABLE MANUFACTURERS;
QUIT;
```

The SAS log shows the SQL statements that were used to create the MANUFACTURERS table as well as an alphabetical list of integrity constraints that have been defined.

## SAS Log Results

```
PROC SQL;
    DESCRIBE TABLE MANUFACTURERS;
NOTE: SQL table WORK.MANUFACTURERS was created like:

create table WORK.MANUFACTURERS( bufsize=4096 )
(
    manunum num label='Manufacturer Number',
    manuname char(25) label='Manufacturer Name',
    manucity char(20) label='Manufacturer City',
    manustat char(2) label='Manufacturer State'
);
create unique index manunum on WORK.MANUFACTURERS(manunum);

    -----Alphabetical List of Integrity Constraints-----
                Integrity
    #   Constraint    Type            Variables
    fffffffffffffffffffffffffffffffffffffffff
    1   PRIM_KEY      Primary Key     manunum

QUIT;
NOTE: PROCEDURE SQL used:
    real time       0.19 seconds
    cpu time        0.01 seconds
```

## Deleting Rows in a Table

In the world of data management, the ability to delete unwanted rows of data from a table is as important as being able to populate a table with data. In fact, data management activities would be severely hampered without the ability to delete rows of data. The DELETE statement and an optional WHERE clause can remove one or more unwanted rows from a table, depending on what is specified in the WHERE clause.

### Deleting a Single Row in a Table

The DELETE statement can be specified to remove a single row of data by constructing an explicit WHERE clause on a unique value. The construction of a WHERE clause to satisfy this form of row deletion may require a complex logic construct. So, be sure to test the expression thoroughly before applying it to the table to determine whether it performs as expected. The following example illustrates the removal of a single customer in the CUSTOMERS table by specifying the customer’s name (CUSTNAME) in the WHERE clause.

## SQL Code

```
PROC SQL;
    DELETE FROM CUSTOMERS2
        WHERE UPCASE(CUSTNAME) = "LAUGHLER";
QUIT;
```

## SAS Log Results

```
PROC SQL;
    DELETE FROM CUSTOMERS2
        WHERE UPCASE(CUSTNAME) = "LAUGHLER";
NOTE: 1 row was deleted from WORK.CUSTOMERS2.
QUIT;
NOTE: PROCEDURE SQL used:
real time                      0.37 seconds
```

### Deleting More Than One Row in a Table

Frequently, a row deletion affects more than a single row in a table. In these cases, a WHERE clause references a value that occurs multiple times. The following example illustrates the removal of a single customer in the PRODUCTS table by specifying the product type (PRODTYPE) in the WHERE clause.

## SQL Code

```
PROC SQL;
    DELETE FROM PRODUCTS
        WHERE UPCASE(PRODTYPE) = `PHONE`;
QUIT;
```

## SAS Log Results

```
PROC SQL;
    DELETE FROM PRODUCTS
        WHERE UPCASE(PRODTYPE) = `PHONE`;
NOTE: 3 rows were deleted from WORK.PRODUCTS.
    QUIT;
NOTE: PROCEDURE SQL used:
real time                      0.05 seconds
```

### Deleting All Rows in a Table

SQL provides a simple way to delete all rows in a table. The following example shows that all rows in the CUSTOMERS table can be removed when the WHERE clause is omitted. Use care when using this form of the DELETE statement because every row in the table is automatically deleted.
