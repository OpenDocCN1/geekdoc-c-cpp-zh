# 4.2 Controlling when a Record Loads

# 4-33

# Execution: First Attempt

```
data salesQL;
infile "&path\sales.dat";
inputID $4. @6 Location $3;
if Location='USA' then
    input @10 Date mmddy10.
    @20 Amount 7;
else if Location='EUR' then
    input @10 Date date9.
    @20 Amount commax7.
run;
```

Invalid data message written to SAS log

Input Buffer
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
30|34   EUR   30|JAN2011   1|876,6|30
PDV
|SaleID | Location | | | Amount |
| $4 | $3 | N8 | N8 |
| 101 | USA | | |

# Execution: First Attempt

```
data salesQL;
infile "&path\sales.dat";
input SaleID $4. @6 Location $3;
if Location='USA' then
    input @10 Date mmddy10.
    @20 Amount 7;
else if Location='EUR' then
    input @10 Date date9.
    @20 Amount commax7.
run;
```

Implicit OUTPUT:
Implicit RETURN;

Input Buffer
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
30|34   EUR   30|JAN2011   1|876,6|30
PDV
|SaleID | Location | | | Amount |
| $4 | $3 | N8 | N8 |
| 101 | USA | | |

Copyright © 2014, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.