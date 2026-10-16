```
ODS CSV CLOSE;
ODS LISTING;
```

# Results

|  | A | B | C | D | E |
|---|---|---|---|---|---|
| 1 | Product Number | Product Name | Manufacturer Number | Product Type | Product Cost |
| 2 | 1110 | Dream Machine | 111 | Workstation | $3,200.00 |
| 3 | 1200 | Business Machine | 120 | Workstation | $3,300.00 |
| 4 | 1700 | Travel Laptop | 170 | Laptop | $3,400.00 |
| 5 | 2101 | Analog Cell Phone | 210 | Phone | $35.00 |
| 6 | 2102 | Digital Cell Phone | 210 | Phone | $175.00 |
| 7 | 2200 | Office Phone | 220 | Phone | $130.00 |
| 8 | 5001 | Spreadsheet Software | 500 | Software | $299.00 |
| 9 | 5002 | Database Software | 500 | Software | $399.00 |
| 10 | 5003 | Wordprocessor Software | 500 | Software | $299.00 |
| 11 | 5004 | Graphics Software | 500 | Software | $299.00 |

Another way of exporting data and output to Microsoft Excel is by using the ODS HTML statement (see the “Delivering Results to the Web” section for details). The HyperText Markup Language (HTML) destination is actually a tagset that contains instructions for importing data and output into the Excel format. In the next example, the ODS HTML statement is specified to import output into a Microsoft Excel spreadsheet file. The resulting XLS file is displayed below in Microsoft Excel.

# SQL Code

```
ODS LISTING CLOSE;
ODS HTML file='sas-to-excel.xls';

PROC SQL;
    SELECT *
        FROM PRODUCTS;
QUIT;

ODS HTML CLOSE;
ODS LISTING;
```