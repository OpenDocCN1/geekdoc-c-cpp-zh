phonetic variations and sounds the same, the results of “Laughler,” “Loffler,” and “Laffler” are spelled differently (illustrated below). The following PROC SQL code uses the sounds-like operator to find all customers that sound like “Lafler.”

# CUSTOMERS2 Table

| CUSTNUM | CUSTNAME | CUSTCITY |
| 1 | Smith | San Diego |
| 7 | Lafler | Spring Valley |
| 11 | Jones | Carmel |
| 13 | Thompson | Miami |
| 7 | Loffler | Spring Valley |
| 1 | Smithe | San Diego |
| 7 | Laughler | Spring Valley |
| 7 | Laffler | Spring Valley |

# SQL Code

```
PROC SQL;
    SELECT CUSTNUM,
            CUSTNAME,
            CUSTCITY
      FROM CUSTOMERS2
     WHERE CUSTNAME =* 'Lafler';
QUIT;
```

# Results

| Customer Number | Customer Name | Customer's Home City |
| 7 | Lafler | Spring Valley |
| 7 | Loffler | Spring Valley |
| 7 | Laffler | Spring Valley |

Readers familiar with the DATA step SOUNDEX(<argument>) function to search a string are cautioned that it cannot be used in an SQL WHERE clause. Instead, the sounds-like operator “=*” must be specified; otherwise, a result of no rows will be selected.

Notice that only three of the four possible phonetic matches were selected in the preceding example (i.e., Lafler, Loffler, and Laffler). The fourth possibility, “Laughler” was not chosen as a “matched” value in the search by the sounds-like algorithm. In an attempt to overcome the inherent limitation with the sounds-like operator, as described in Joe Celko’s popular book SQL for Smarties: Advanced SQL Programming (Morgan Kaufman, 1999), and to derive a broader list of “matched” values, programmers should make every attempt to develop a comprehensive list of search values to widen the scope of possibilities. We can expand our original search criteria in the previous example to include the missing possibilities using OR logic.