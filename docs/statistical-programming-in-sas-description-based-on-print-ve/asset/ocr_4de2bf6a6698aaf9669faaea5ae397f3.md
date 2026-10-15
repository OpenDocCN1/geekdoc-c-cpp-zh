# Display 1.3 *(continued)*

```
NOTE: PROCEDURE PRINT used (Total process time):
      real time          2.27 seconds
      cpu time           0.29 seconds

11
12  ods rtf bodytitle file="C:\Users\baileraj.IT\Desktop\ch1-display-1.2-fig.rtf";
NOTE: Writing RTF Body file: C:\Users\baileraj.IT\Desktop\ch1-display-1.2-fig.rtf
13  ods graphics on;
14  proc reg data=lin_reg_data plots(only)=FitPlot(nolimits);
15      model y=x;
16  run;

17  ods graphics off;
18  ods rtf close;
```

The output from PROC PRINT is shown in Display 1.4, and the output from the ODS RTF statement and PROC REG is shown in Display 1.5. For more information about fitting regression models, see Chapter 5.

# Display 1.4  Output produced by PROC PRINT

| The SAS SystemObs | x | y |
|---:|---:|---:|
| 1 | 1 | 6.1693 |
| 2 | 2 | 5.8702 |
| 3 | 3 | 10.5551 |
| 4 | 4 | 6.9707 |
| 5 | 5 | 12.0795 |
| 6 | 6 | 14.8699 |
| 7 | 7 | 17.9952 |
| 8 | 8 | 19.1788 |
| 9 | 9 | 17.7443 |
| 10 | 10 | 24.5809 |

Display 1.4 is the output from PROC PRINT that is copied from the output window in an interactive SAS session. This would be the contents of a .lst or .listing file that would be produced if batch SAS were used to execute the program in Display 1.2.

Display 1.5 is the output from PROC REG and is structured as a series of tables in a rich text format. Each section of the output is an object that can be separately extracted. (This is discussed in Chapter 4.) ODS graphics associated with the REG procedure produces the scatter plot with the fitted regression line in Display 1.5.