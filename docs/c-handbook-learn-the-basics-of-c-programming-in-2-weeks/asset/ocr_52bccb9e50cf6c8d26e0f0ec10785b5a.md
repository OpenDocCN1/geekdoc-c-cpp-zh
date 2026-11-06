# The Constraints in SQL

In SQL, a constraint is a rule applied on certain data columns. It is used to restrict the kind of information that can be stored in the table. Basically, constraints help you in ensuring the reliability and accuracy of your databases.

You can apply constraints on a tabular or columnar level. Thus, you may apply constraints on certain columns or entire tables.

Here are some of the popular constraints in the SQL programming language:

+   - UNIQUE – This constraint prevents data redundancy in your selected columns. For instance, you may need to prevent listed users from having the same identification number. Analyze the following example:

```
CREATE TABLE CUSTOMERS(
  ID INT NOT NULL,
  NAME VARCHAR (20) NOT NULL,
  AGE INT NOT NULL UNIQUE,
  ADDRESS CHAR (25) ,
  SALARY DECIMAL (18, 2),
  PRIMARY KEY (ID)
);
```

This code creates a table named CUSTOMERS and divides it into five columns. The UNIQUE constraint is applied on the AGE column, so you can’t enter two or more customers with identical age.

If you want to apply this constraint on an existing column, you may use the following syntax:

```
ALTER TABLE (insert name of table here)
    MODIFY (insert name of column) (specify the value type) NOT NULL UNIQUE;
```

+   - DEFAULT – This constraint allows you to set default data. However, you can only use this if INSERT INTO (another SQL statement) doesn’t have a particular