put the ods graphics on statement at the beginning of your SAS program if you want ODS Graphics to be produced by more than one procedure. Note: ODS Graphics consume additional resources (time and memory), which is why it is not the default way to produce graphics.

# Display 6.1 Generating a cubic mean response data set and fitting a linear regression model with ODS Graphics requested

```
data cubic;
    call streaminit(8675309);
    do nrep=1 to 3;
        do x=1 to 10;
            response = 3 + 1*x - .5*x**2 + .05*x**3 + rand('normal',0,1.5);
            output;
        end;
    end;
run;

ods rtf bodytitle file="C:\Users\baileraj.IT\Desktop\fig6p1.rtf";
ods trace on;
ods graphics on;
proc reg data=cubic;
    model response = x;
run;
ods graphics off;
ods trace off;
ods rtf close;
```

The ODS Graphics produced by default with PROC REG are shown in Displays 6.2A, 6.2B, and 6.2C. A fit diagnostics panel in Display 6.2A, a plot of residuals versus the predictor variable in Display 6.2B, and the fitted model with confidence and prediction intervals in Display 6.2C are produced.