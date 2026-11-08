The DSD option on the FILE statement ❷ implies a comma as the delimiter, although the DLM= option can be used to specify a different option (see Section 1.4.1). The _ALL_ list abbreviation can still be used; however, a neutral modifier must also be selected. Either the colon (:) or the question mark (?) ❸, will serve the purpose.

```
```sas
data _null_;
    set avdata.demog(keep=fname lname dob);
    file csv_b dsd; ❷
    if n = 1 then put 'FName,LName,DOB';
    put (_all_) (?) ❸;
    run;
```
```

Because the DSD option has been used, an approach such as this one will also work when one or more of the variables contain an embedded delimiter.

# 1.5 SQL Pass-Through

SQL pass through allows the user to literally pass instructions through a SAS SQL step to the server of another database. Passing code or SQL instructions out of the SQL step to the server can have a number of advantages, most notably significant efficiency gains.

# 1.5.1 Adding a Pass-Through to Your SQL Step

The pass-through requires three elements to be successful:

+   - A connection must be formed to the server/database. ❶
+   - Code must be passed to the server/database. ❷
+   - The connection must be closed. ❸

These three elements will be formulated as statements (❶ CONNECT and ❸ DISCONNECT) or as a clause within the FROM CONNECTION phrase ❷.

```
```sas
proc sql noprint;
    connect to odbc (dsn=clindat uid=Susie pwd=pigtails); ❶

    create table stuff as select * from connection to odbc (
        select * from q.org ❷
            for fetch only
    );

    disconnect from odbc; ❸
quit;
```
```

The connection that is established using the CONNECT statement ❶ and is then referred to in the FROM CONNECTION TO phrase.

Notice that the SQL code that is being passed to the database, not a SAS database, ❷ is within the parentheses. This code must be appropriate for the receiving database. In this case the pass through is to a DB2 table via an ODBC connection.

There are a number of types of connections and while ODBC connections, such as the one established in this example, are almost universally available in the Microsoft/Windows world, they are typically slower than SAS/ACCESS connections.