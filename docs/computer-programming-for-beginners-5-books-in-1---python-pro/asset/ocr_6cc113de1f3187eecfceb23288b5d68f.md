![](bbox=[0.034, 0.026, 0.962, 0.469])

This shows that the primary key was dropped successfully.

# Foreign Key

This constraint is used to link two tables together. Sometimes, it is referred to as a referencing key. The foreign key is simply a column or a set of columns that match a Primary Key in another table.

Consider the tables with the structures given below:

STUDENTS table:

```
```sql
CREATE TABLE STUDENTS(
    ADMISSION INT NOT NULL,
    NAME VARCHAR (15) NOT NULL,
    AGE INT NOT NULL,
    PRIMARY KEY (ADMISSION)
);
```
```

FEE table:

```
```sql
CREATE TABLE FEE (
```
```