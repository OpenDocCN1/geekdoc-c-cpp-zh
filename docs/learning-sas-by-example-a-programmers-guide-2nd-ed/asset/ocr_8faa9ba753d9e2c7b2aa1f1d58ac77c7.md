# Program 8.4: Creating a Cumulative Total with the RETAIN Statement (Second Attempt)

```
data Revenue;
  retain Total 0;
  input Day : $3;
  Revenue : dollar6;
Total = Total + Revenue; /* Note: this does not work */
format Revenue Total dollar8;
datalines
Mon $1,000
Tue $1,500
Wed
Thu $2,000
Fri $3,000
;

title "Listing of Revenue"
proc print data=Revenue nobs;
run;
```

In this program, Total is retained and initialized at 0. Here is the output:

Figure 8.3: Output from Program 8.4

| Total | Day | Revenue |
|---|---|---|
| $1,000 | Mon | $1,000 |
| $2,500 | Tue | $1,500 |
| | Wed | - |
| | Thu | $2,000 |
| | Fri | $3,000 |

Everything works fine until the program encounters a missing value for Revenue. This sets Total to a missing value, where it remains for the rest of the DATA step. You can fix this by adding a statement to test the value of Revenue before you attempt to add it to the cumulative Total, like this: