The probabilities and density produced by Display 8.51 are shown in Display 8.52. This display includes the binomial Pr(Y=m) and the standard normal density evaluated at z=0, normal_density_0 = 0.399 (= 1/√2π =0.399).

# Display 8.52 Output from PROC PRINT of normal and binomial PDF function

| bin_0 | bin_1 | bin_2 | bin_3 | bin_4 | normal_density_0 |
| 0.0625 | 0.25 | 0.375 | 0.25 | 0.0625 | 0.39894 |

Suppose you want to generate a graphical comparison of t(df=4) with a standard normal density. The following program might be useful.

# Display 8.53 Comparing a standard normal density to t₄

```
data t_vs_z;
 do x= -3.5 to 3.5 by .001;
  t4 = x;
  t_density = PDF('t', x, 4);
  z = x;
  z_density = PDF('Normal', x);
  output;
 end;
run;

ods rtf bodytitle file="C:\Users\baileraj.IT\Desktop\Display-8-54.rtf";

ods graphics on;
proc sgplot data=t_vs_z;
 label t_density="t[df=4] density";
 label z_density="N(0,1) density";
 series x=t4 y=t_density / curvelabel;
 series x=z y=z_density / curvelabel;
 xaxis label="value";
 yaxis label="density";
run;
ods graphics off;
ods rtf close;
```

Comparing the standard normal density to t₄ is shown in Display 8.54.