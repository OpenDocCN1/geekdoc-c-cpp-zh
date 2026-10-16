The inserted row of data from the INSERT INTO statement and SET clause is added to the end of the CUSTOMERS table.

|  | Customer Number | Customer Name | Customer's Home City |
|---|---|---|---|
| 1 | 101 La Mesa Computer Land | La Mesa |
| 2 | 201 Vista Tech Center | Vista |
| 3 | 301 Coronado Internet Zone | Coronado |
| 4 | 401 La Jolla Computing | La Jolla |
| 5 | 501 Alpine Technical Center | Alpine |
| 6 | 601 Oceanside Computer Land | Oceanside |
| 7 | 701 San Diego Byte Store | San Diego |
| 8 | 801 Jamul Hardware & Software | Jamul |
| 9 | 901 Del Mar Tech Center | Del Mar |
| 10 | 1001 Lakeside Software Center | Lakeside |
| 11 | 1101 Bonsall Network Store | Bonsall |
| 12 | 1201 Rancho Santa Fe Tech | Rancho Santa Fe |
| 13 | 1301 Spring Valley Byte Center | Spring Valley |
| 14 | 1401 Poway Central | Poway |
| 15 | 1501 Valley Center Tech Center | Valley Center |
| 16 | 1601 Fairbanks Tech USA | Fairbanks Ranch |
| 17 | 1701 Blossom Valley Tech | Blossom Valley |
| 18 | 1801 Chula Vista Networks |  |
| 19 | 702 Mission Valley Computing | San Diego |

Entering a new row into a table containing an index will automatically add the value to the index (for more information about indexes, see Chapter 6, “Modifying and Updating Tables and Indexes”). The following example illustrates adding three rows of data using the SET clause.

# SQL Code

```
PROC SQL;
    INSERT INTO CUSTOMERS
        SET CUSTNUM=402,
            CUSTNAME='La Jolla Tech Center',
            CUSTCITY='La Jolla'
        SET CUSTNUM=502,
            CUSTNAME='Alpine Byte Center',
            CUSTCITY='Alpine'
        SET CUSTNUM=1702,
            CUSTNAME='Rancho San Diego Tech',
            CUSTCITY='Rancho San Diego';
    QUIT;
```

The SAS log shows that three rows of data were inserted into the CUSTOMERS table.