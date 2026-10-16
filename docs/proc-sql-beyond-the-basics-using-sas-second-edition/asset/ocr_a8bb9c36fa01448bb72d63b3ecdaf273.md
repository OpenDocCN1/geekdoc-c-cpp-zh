second table. As illustrated in Figure 7.4, the results of specifying the EXCEPT operator represent the shaded area (A).

# Figure 7.4: Compare Two Tables to Determine Additions and Changes

![](bbox=[0.4, 0.25, 0.61, 0.41])

When working with two tables that consist of similar information, you can use the EXCEPT operator to determine new and modified rows. The EXCEPT operator is used to identify rows in the first table (or query), but is not used to identify rows in the second table (or query). It also uniquely identifies rows that have changed from the first table to the second table. Columns are compared in the order that they appear in the SELECT statement.

If the wildcard character “*” is specified in the SELECT statement, it is assumed that the tables are structurally identical to one another. Let’s look at an example.

Suppose that you have master and backup tables of the CUSTOMERS file, and you want to compare them to identify the new and changed rows. The EXCEPT operator as illustrated in the next example returns all new or changed rows from the CUSTOMERS table that do not appear in the CUSTOMERS_BACKUP table. As illustrated in the results, three new customer rows are added to the CUSTOMERS table that had not previously existed in the CUSTOMERS_BACKUP table.

# SQL Code

```
PROC SQL;
    SELECT *
        FROM CUSTOMERS_BACKUP
    EXCEPT
    SELECT *
        FROM CUSTOMERS;
QUIT;
```

1 The EXCEPT operator compares rows in both tables to identify the rows existing in the first table but not the second table.