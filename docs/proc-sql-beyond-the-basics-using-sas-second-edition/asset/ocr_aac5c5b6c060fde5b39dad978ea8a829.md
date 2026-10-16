# SQL Code

```
PROC SQL VERBOSE;
    SELECT products.prodname,
        products.prodtype,
        customers.custname,
        manufacturers.manuname
    FROM MANUFACTURERS,
        PRODUCTS,
        INVOICE,
        CUSTOMERS
    WHERE manufacturers.manunum = products.manunum  AND
        manufacturers.manunum = invoice.manunum  AND
        products.prodnum      = invoice.prodnum  AND
        invoice.custnum       = customers.custnum;
QUIT;
```

As illustrated in the following SAS log, information pertaining to the number of input rows along with the logical record length (LRECL) is produced for each table when the VERBOSE SQL procedure option is specified.

# SAS Log Results

```
PROC SQL VERBOSE;
    SELECT P.prodname,
        P.prodtype,
        C.custname,
        M.manuname
    FROM MANUFACTURERS  M,
        PRODUCTS        P,
        INVOICE         I,
        CUSTOMERS       C
    WHERE M.manunum = P.manunum  AND
        M.manunum = I.manunum  AND
        P.prodnum = I.prodnum  AND
        I.custnum = C.custnum;
Data Set Tags.
Data Set WORK.MANUFACTURERS is num=1 and tag=0001. NOBS=6, lrecl=50.
Data Set WORK.PRODUCTS is num=2 and tag=0002. NOBS=10, lrecl=51.
Data Set WORK.INVOICE is num=3 and tag=0004. NOBS=7, lrecl=20.
Data Set WORK.CUSTOMERS is num=4 and tag=0008. NOBS=18, lrecl=48.
QUIT;
```

# Identifying Tables with the Most Indexes

Database administrators and user support staff are concerned with the installation, configuration, administration, monitoring, and maintenance of the database environment, and consequently take special interest in a variety of activities including the performance and health of database applications. It is particularly important for them to be aware of issues that could impact future expansion requirements. One thing that can affect I/O and storage performance is a large number of indexes in a database environment. For this reason, I often find it valuable to know how many