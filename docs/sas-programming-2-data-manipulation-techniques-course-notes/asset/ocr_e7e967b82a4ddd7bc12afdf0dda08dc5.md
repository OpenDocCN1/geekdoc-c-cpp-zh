# Desired Output

work.salesQ1

| Sale ID | Location | Date | Amount |
| --- | --- | --- | --- |
| 101 | USA | 18647 | 3295.50 |
| 3034 | EUR | 18657 | 1876.30 |
| 101 | USA | 18657 | 2938.00 |
| 128 | USA | 18663 | 2908.74 |
| 1345 | EUR | 18664 | 3145.60 |
| 109 | USA | 18703 | 2789.10 |

# Mixed Record Types: First Attempt

This code is a good start to reading the mixed record types, but it gives unexpected results.

```
data salesQ1;
infile "&path\sales.dat";
in inputID $4. @6 Location $3;
if Location='USA' then
  input @10 SaleDate mddyym10;
  @20 Amount 7;
else if Location='EUR' then
  input @10 SaleDate date9;
  @20 Amount commax7;
run;
```