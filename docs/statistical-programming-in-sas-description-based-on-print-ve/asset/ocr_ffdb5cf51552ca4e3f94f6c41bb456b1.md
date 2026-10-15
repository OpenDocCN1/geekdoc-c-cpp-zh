order terms for a polynomial regression, and the construction of indicator variables. Two of these tasks are highlighted using the nitrofen data³ as coded in Display 8.18.

# Display 8.18 Data transformations before fitting a polynomial regression model

```
data nitrofen;
infile 'C:\Users\baileraJ.IT\Desktop\ch2-dat.txt' firstobs=16 expandtabs;
input 017 conc 3. 049 total 2.;
sqrt_total = sqrt(total); * transformed response variable;
cconc = conc - 157; * construct mean-centered concentration;
cconc2 = cconc*cconc; * quadratic term;
run;
ods rtf BODYTITLE file="C:\Users\baileraJ.IT\Desktop\Display-8-18.rtf";
ods graphics on;
proc reg data=nitrofen;
model sqrt_total = cconc cconc2; * fit the polynomial reg. model;
run;
ods graphics off;
ods rtf close;
```

The mean-centered concentration was determined in a different program and hard coded here. (It would be slick to use PROC STANDARD to construct a variable containing the mean-centered version of the concentration variable, which you then output to a new data set. Can you figure out how to do this at home?) Even more interesting alternatives to the DATA step programming of the transformation include the following:

+   - PROC GLM with MODEL SQRT_TOTAL=CONC | CONC;
+   - PROC TRANSREG with MODEL POWER(TOTAL / PARAMETER=0.5)=PSPLINE(CONC / CENTER DEGREE=2);

ODS graphics associated with this fitted polynomial regression model are shown in Display 8.19.

> ³ Nitrofen data set from Bailer, A. John., and James T. Oris. 1994. "Assessing Toxicity of Pollutants in Aquatic Systems." Chapter 2 in Case Studies in Biometry. Nicholas Lange, Louise Ryan, Lynne Billard, David Brillinger, Loveday Conquest, Joel Greenhouse, eds. New Jersey: John Wiley & Sons, Inc. Reprinted with permission of John Wiley & Sons, Inc.