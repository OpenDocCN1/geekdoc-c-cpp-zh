# First Attempt: Unexpected Output

```
proc print data=salesQ1 noobs;
run;
```

| Sale ID | Location | Date | Amount |
|---|---|---||}{
| 101 | USA | 18663 | 2908.74 |
| 101 | USA | | 27891.00 |
| 1345 | EUR | | |

To get the correct results, SAS needs some way to keep the second INPUT statement from moving to the next line of raw data.

# Mixed Record Types: Correct Program

The single trailing @ holds a raw data record in the input buffer until SAS does one of the:

+   - executes an INPUT statement with no trailing @
- begins the next iteration of the DATA step

```
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @;
if Location='USA' then
 input @10 Date mmmddy10.
 @20 Amount 7.;
else if Location='EUR' then
 input @10 Date date9.
 @20 Amount commax7.;
run;
```

Normally, each INPUT statement in a DATA step reads a new data record into the input buffer. When you use a trailing @ the following occur:

+   - The pointer position does not change.
- No new record is read into the input buffer.
- The next INPUT statement for the same iteration of the DATA step continues to read the same record rather than a new one.