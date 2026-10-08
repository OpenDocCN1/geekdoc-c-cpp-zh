# 5.01 Short Answer Poll

Which SAS functions have you used?

# Using SAS Functions (Review)

You can use functions in DATA step statements anywhere that an expression can appear.

```
data contrib;
  set orion.employee donations;
  Total=sum(Qtr1,Qtr2,Qtr3,Qtr4);
  if Total ge 50;
run;
function-name(argument-1,argument-2,...,argument-n)
proc print data=contrib noobs;
  title 'Contributions $50 and Over';
  var Employee_ID Qtr1 Qtr2 Qtr3 Qtr4
  Total;
run;
```