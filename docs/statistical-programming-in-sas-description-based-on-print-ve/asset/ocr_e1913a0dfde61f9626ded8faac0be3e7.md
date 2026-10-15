An interesting construct in this program is &&&variable.&obs. Macro variable names are resolved from left to right. && is resolved to & by the macro processor. In this example, when &variable=var1 (=week) and &obs=time1 (=1), &&&variable.&obs has the value var1time1 (=week1). The SAS log from invoking this macro is shown in Display 10.9.

# Display 10.9 Output from invoking the macro

```
%showvalue(variable=var1, obs=time1)
Value of '&variable' = var1
Value of '&obs' = time1
Value of '&&&variable.&obs' = week1
```

In the macro defined in Display 10.10 (trap_area_Z), a macro wrapper is placed around the trapezoidal rule area estimator code. Parameters are defined for this macro: LOW, HIGH, npts_lo, npts_hi, npts_by, fout, print_est, print_pts, display_graph, and ODS_on. The macro declaration for trap_area_Z includes these parameters and their default values.

```
%macro trap_area_Z
(LOW=-1.645,HIGH=1.645,npts_lo=10,npts_hi=10,npts_by=2,
fout=C:\Users\baileraj.IT\Desktop\est3.out,
print_est=FALSE, print_pts=FALSE, display_graph=FALSE,
ODS_on=FALSE);
```

In contrast to the positional parameters in Display 10.8, keyword parameters are used in the trap_area_Z macro definition. Parameters can be passed by position, by keyword, or by using a mix of the two strategies. (If a mix is used, then positional parameters must be specified before keyword parameters.) If you define a keyword parameter, then you must call the macro with a keyword in the argument list. The style used in the macro definition needs to match the style used when invoking the macro. In the spirit of writing self-documenting code, keyword parameters are preferred.

The construction of the trap_area_Z macro explicitly addresses two questions:

+   1. Can you set up a switch to produce graphics only when they are requested?
+   2. Is it possible to package this estimator as a callable program, subroutine, or function?

Let’s start with the name of this macro and its input parameters. The input parameters are assigned default values in the macro. Macro comments describe the input parameters. These comments begin with a %* and end with a semicolon. If you use standard comments (e.g., you start with an asterisk and end with a semicolon), the comments are