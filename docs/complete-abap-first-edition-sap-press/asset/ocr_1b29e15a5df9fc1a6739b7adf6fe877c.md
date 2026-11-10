```
DATA : it_vbrk TYPE STANDARD TABLE OF ty_vbrk,
       wa_vbrk TYPE ty_vbrk.

*Selecting a single row of specific fields from table vbrk.
SELECT SINGLE vbeln fkdat netwr kunrg FROM vbrk
                                  INTO wa_vbrk
                                  WHERE vbeln EQ '9000'.
```

**Listing 5.23** Using SELECT SINGLE

Listing 5.24 uses SELECT...ENDSELECT to fetch all matching rows, one row at a time. The system loops between SELECT...ENDSELECT, transferring one row at a time to the structure wa_vbrk. You can process the contents of wa_vbrk in each loop by writing the statements before ENDSELECT. This is an efficient way to process the records from the database table if you plan to use a database table only once during program execution.

However, if you plan to reuse the data multiple times during the life of the program execution, we recommend using internal tables, which allows you to fetch the data once into your program and access it subsequently multiple times, as opposed to accessing the database every time you need the same data.

```
*Selecting all matching rows of specific fields from the table
*vbrk using a structure.
*Here the system fetches one row at a time and loops between
*select...endselect. The row can be processed between SELECT...ENDSELECT.
SELECT vbeln fkdat netwr kunrg FROM vbrk
                         INTO wa_vbrk
                         WHERE vbeln EQ '9000'.

ENDSELECT.
```

**Listing 5.24** Using SELECT...ENDSELECT

Listing 5.25 shows using an internal table in a SELECT statement, also known as performing an array fetch. Once the SELECT statement is executed, you can access the data from the internal table as discussed previously.

```
*Selecting all matching rows of specific fields from the table
*vbrk using an internal table.
SELECT vbeln fkdat netwr kunrg FROM vbrk
                         INTO TABLE it_vbrk
                         WHERE vbeln EQ '9000'.
```

**Listing 5.25** Selecting Data to Internal Table