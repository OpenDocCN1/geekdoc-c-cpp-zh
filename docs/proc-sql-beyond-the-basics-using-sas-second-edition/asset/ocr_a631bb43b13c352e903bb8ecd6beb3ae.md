# Results

# The SAS System

| Product Name | Product Cost | Sales_Tax |
| Dream Machine | $3,200.00 | 240 |
| Business Machine | $3,300.00 | 247.5 |
| Travel Laptop | $3,400.00 | 255 |
| Analog Cell Phone | $35.00 | 2.625 |
| Digital Cell Phone | $175.00 | 13.125 |
| Office Phone | $130.00 | 9.75 |
| Spreadsheet Software | $299.00 | 22.425 |
| Database Software | $399.00 | 29.925 |
| Wordprocessor Software | $299.00 | 22.425 |
| Graphics Software | $299.00 | 22.425 |

The next example illustrates the second method of assigning a column heading for the computed sales tax column with the LABEL= option. To further enhance the output’s readability, a numeric dollar format is specified.

Note: Because the next example is a query and the table is not being updated, the assigned attributes are only available for the duration of the step and are not permanently saved in the table’s record descriptor.

# SQL Code

```
PROC SQL;
    SELECT prodname, prodcost,
        .075 * prodcost FORMAT=DOLLAR7.2
            LABEL='Sales Tax'
    FROM PRODUCTS;
QUIT;
```