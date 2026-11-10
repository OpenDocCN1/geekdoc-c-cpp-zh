```
FLDATE TYPE S_DATE.
END OF ty_sflight.
DATA : it_sflight TYPE TABLE OF ty_sflight,
       wa_sflight TYPE ty_sflight.
```

**Listing 5.7** Defining Internal Table Work Area

**Figure 5.11** depicts the usage of a work area. Because the work area can store only one record, you can read a single row from the internal table or loop through all rows of the table one row at a time.

To read a single record from the internal table, use the READ statement, and to process more than one record, use the LOOP statement. The READ and LOOP statements copy the data from the internal table to the work area.

![](bbox=[0.148, 0.362, 0.624, 0.519])

**Figure 5.11** Internal Table and Work Area

There are a couple of ways to access a single record from an internal table via the READ statement. You can use an index (index access) or you can read the table by comparing the value of a field (or a set of fields) of the row (key access). Please note that not all internal tables support index access, which we will discuss in the next section.

**Listing 5.8** shows example code to read an internal table using index access.

```
TYPES : BEGIN OF ty_sflight.
         CARRID TYPE S_CARRID,
         CONNID TYPE S_CONN_ID,
         FLDATE TYPE S_DATE,
       END OF ty_sflight.
DATA : it_sflight TYPE TABLE OF ty_sflight,
       wa_sflight TYPE ty_sflight.

SELECT carrid connid fldate FROM sflight INTO TABLE it_sflight.

*Reading a single record from the internal table into work area
```