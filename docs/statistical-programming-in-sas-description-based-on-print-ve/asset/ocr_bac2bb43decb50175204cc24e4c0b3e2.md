The transposed data set tran_out has one row and 20 columns (variables xx1 through xx20) containing the totals and a variable _NAME_, which has the value TOTAL (i.e., the name of the variable that is transposed).

# Display 9.8 Constructing a randomization test of two-population mean equality

```
data test;
  input Obs conc total;     * entering directly as alternative to ;
  datalines;                * permanent SAS data file reference;
  1     0    27
  2     0    32
  3     0    34
  4     0    33
  5     0    36
  6     0    34
  7     0    33
  8     0    30
  9     0    24
 10     0    31
 11   160    29
 12   160    29
 13   160    23
 14   160    27
 15   160    30
 16   160    31
 17   160    30
 18   160    26
 19   160    29
 20   160    29
;
run;

proc print data=test;
  title "NITROFEN: print of (0, 160) concentrations";
  var conc total;
run;

proc transpose data=test prefix=xx out=tran_out;
  var total;
run;

* add variable "type" to identify the observed data;
data obs_test; set tran_out;
  type = "O";     * identifies original data;
run;
```