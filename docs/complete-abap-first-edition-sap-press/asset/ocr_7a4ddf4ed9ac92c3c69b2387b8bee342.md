can't use `APPEND` statements with hashed tables, because they only support `INSERT` statements.

Listing 5.14 shows an example of using the `APPEND` statement to add records to a standard table. To add a record to an internal table, first fill the work area with the required data and then append it to the table using the `APPEND` statement.

```
```abap
*Adding a record to internal table
TYPES : BEGIN OF ty_sflight,
          CARRID TYPE S_CARR_ID,
          CONNID TYPE S_CONN_ID,
          FLDATE TYPE S_DATE.
        END OF ty_sflight.
DATA : it_sflight TYPE STANDARD TABLE OF ty_sflight,
       wa_sflight TYPE ty_sflight.

*You can't refer to the table row directly to add a record.
*Fill the work area with the values and add it to the table.
wa_sflight-carrid = 'AA'.
wa_sflight-connid = '0004'.
wa_sflight-fldate = '20140101'.
APPEND wa_sflight TO it_sflight. "Adds the first row to the table

wa_sflight-carrid = 'AB'.
wa_sflight-connid = '0005'.
wa_sflight-fldate = '20140102'.
APPEND wa_sflight TO it_sflight. "Adds second row to the table
```
```

# Listing 5.14 Using APPEND Statement to Add Records Into Internal Table

Listing 5.15 shows an example using the `INSERT` statement. Notice the difference in the syntax compared to the `APPEND` statement. The listing shows the usage of the `INSERT` statement with and without an explicit index. When an index is supplied with the `INSERT` statement, the record is added explicitly in that row.

If the index supplied is greater than the line of the table, no record is inserted and the system field `sy-subrc` is set to 4. Refer to the box ahead for an explanation of system fields.

```
```abap
*The following code inserts the record as last row
wa_sflight-carrid = 'AC'.
wa_sflight-connid = '0006'.
wa_sflight-fldate = '20140103'.
INSERT wa_sflight INTO TABLE it_sflight.
*The following code inserts the record at a specific position based on
*the index.
wa_sflight-carrid = 'AD'.
```
```