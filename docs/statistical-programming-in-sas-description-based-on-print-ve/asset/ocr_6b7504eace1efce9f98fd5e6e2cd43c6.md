# Display 8.36 (continued)

```
proc ttest data= simulate 2group t;
  by iexpt;
  class group;
  var Y;
run;
ods output close;

/* accumulate results over numerous simulated data sets */

data out_ttests; set out_ttests;
retain Pooled_p;  * RETAIN explained in Section 8.3;
if method="Pooled" then Pooled_p = Probt;
else do;
  Satter_p = Probt;
  Pooled_reject = (Pooled_p <= 0.05); * Boolean trick again;
  Satter_reject = (Satter_p <= 0.05);
  keep iexpt Pooled_p Satter_p Pooled_reject Satter_reject;
  output;
end;
run;

ods rtf bodytitle file="C:\Users\baileraj.IT\Desktop\Display-8-37.rtf";
proc freq;
  table Pooled_reject Satter_reject;
run;
ods rtf close;
```

The pooled variance t-test and the Satterthwaite adjustment reject 4.98% and 4.83% of the time, respectively, when the null hypothesis is true and the data are from normal populations with homogeneous variances. These rejection rates are based on 4000 simulated experiments. The bound on the Monte Carlo error of estimation is approximately the following:

$B = 2\sqrt{\frac{(0.05)(0.95)}{4000}} = 0.007$

This suggests that a procedure operating at α=0.05 would have an observed Type I error rate between 0.043 and 0.057 in the case where 4000 simulated experiments are considered.

If you repeat this program, but change SIG 2=2 and hold all other variables constant (i.e., the second population has a variance that is four times greater than the first population), you observe 5.33% and 4.83% Type I error rates in the pooled variance t-test and separate variance t-test, respectively. Try this at home.