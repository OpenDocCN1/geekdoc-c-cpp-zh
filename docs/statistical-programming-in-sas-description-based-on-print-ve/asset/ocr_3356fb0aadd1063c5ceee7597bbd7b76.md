# Display 3.27 Using PROC SGPLOT to produce a histogram with superimposed density

```
%let DATA_DIR = C:\Users\baileraj.IT\Desktop;
data nitro_tox;
  infile "&DATA_DIR\ch2-dat.txt"
    firstobs=16 expandtabs missover pad ;
  input @9 animal 2. @17 conc 3. @25 brood1 2.
        @33 brood2 2. @41 brood3 2. @49 total 2.;
run;

*ods rtf style=journal bodytitle
    file="&DATA_DIR\Display-3.27.rtf";  * selecting gray scale style/
B&W;

ods listing image dpi=300 style=journal;
ods graphics / width=4.5in;
proc sgplot data=nitro_tox;          * figure as often used in journal
                                     articles;
  histogram total;
  density total / type=kernel;
  keylegend / location=inside position=topleft;
run;
ods graphics off;
*ods rtf close;
```

# Display 3.28 Histogram with superimposed density produced by PROC SGPLOT

![](bbox=[0.09, 0.58, 0.75, 0.89])