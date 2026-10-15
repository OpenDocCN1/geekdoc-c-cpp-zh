
# Display 10.4 Output containing the [x,f(x)] values used in the trapezoidal rule

![](img/26474180ee55914c13fb9156a7678157_371_0.png)

You have a specific implementation for a particular problem. What can you do with this implementation? Consider the following questions:

- 1. How hard is it to modify this code if you want k=50 points versus k=25 points?
- 2. Can you generalize this code to specify different limits of integration?
- 3. Can you set up a switch to produce graphics only when they are requested?
- 4. Is it possible to package this estimator as a callable program, subroutine, or function?
- 5. Can you generalize this code for any arbitrary function?

For the impatient, the answers to these questions are: not too hard, easily, easily, yes, and yes. The common denominator in all of these answers is macros.

## 10.3 Processing Macros

“You talkin’ to me? You talkin’ to me? You talkin’ to me?” says Travis Bickle in the film Taxi Driver.

The macro processor is the Travis Bickle of SAS. To understand why, look at how SAS processes a program in the following short overview. If you want a more detailed description, see Introduction to SAS Programs and Macro Processing at support.sas.com, or Burlew (2006).

When program statements are submitted, they are sent to the input stack, which is an area of computer memory. The word scanner processes these program statements by converting them to tokens. Tokens are directed to an appropriate location for additional processing. Appropriate locations include the DATA step compiler, command processor, and macro processor. If a program contains any macro statements, then SAS sets up a symbol table for the macro variables. (Actually, SAS defines certain macro variables every time you use it. For example, the day that you run SAS is a value stored in a macro variable named SYSDAY). SAS needs to resolve any macro requests that are part of a series of commands before these commands are processed. So, how does the word scanner know how to direct tokens to an appropriate location? Any non-blank text that is preceded by a percentage sign (%) or ampersand (&) is a macro trigger. When the word scanner encounters a macro trigger, it sends the tokens with % or & to the macro processor. (So, “you are talkin’” to the macro processor if you are text that contains a macro trigger.) The macro processor interacts with the symbol table to store or extract the values of macro variables. Or, more generally, the macro processor interacts with the word scanner to resolve any macro statements. The macro processor substitutes the text demanded of it from the macro statements into the input stack. This continues until the input stack has been completely processed. All of this will become clearer when you look at how code with macro statements and variables is resolved.

## 10.4 Macro Variables, Parameters, and Functions

A macro variable can be referenced anywhere in a SAS program. (The only exception is in data lines that are being read into SAS.) A macro variable can be assigned text values. The value of a variable is stored in either a local or global symbol table. A macro variable name must be a valid SAS name. (#$#% @#$%#! won’t work, even though you might feel this way about a programming project.) A macro variable is preceded by an & when it is referenced in a SAS program. When a macro variable is resolved in a program, it might be closely associated with text. If it follows text, then it is referenced as text&macro-variable. If it precedes text, then it is referenced with a period delimiting the

value from the text (&macro-variable.text). SAS can define certain macro variables (automatic macro variables), while a program can define other macro variables (user-defined macro variables.)

When you first start macro programming in SAS, you will most likely use macro variables to define simple substitutions in a program. In Display 10.5, the trapezoidal numerical integration routine is modified to address the previous questions.

- 1. How hard is it to modify this code if you want k=50 points versus k=25 points?
- 2. Can you generalize this code to specify different limits of integration?

The macro statement %let assigns values to npts (the macro variable for k), and to low and high (the macro variables that correspond to the limits of integration). In the following code, every occurrence of 25 in the program is replaced with &npts. Every occurrence of 24 is replaced with &npts-1. Because you can specify any arbitrary number of points to be evaluated in this numerical integration, the first question is answered. Including macro variables &LOW and &HIGH generalizes the code to specify different limits of integration. As a result, the second question is answered. These macro variables are incorporated into titles in this modified program. Additional bells and whistles are added, including using a put statement to write the results, and using a file statement to specify a location for the put output.

# Display 10.5 Replacing the limits of integration and number of points to evaluate

```
/* Estimate P(low < Z < high) using the trapezoidal rule */
%let npts = 50;
%let LOW = -1.645;
%let HIGH = 1.645;

data trapper;
  file "C:\Users\baileraj.IT\Desktop\est.out" MOD;
  trapsum = 0;
  array x_value(&npts) x1-x&npts;
  array f_value(&npts) y1-y&npts;

  low = &LOW;
  high = &HIGH;
  incr = (high-low)/( &npts -1);
  pi = arcos(-1);
  do i = 1 to &npts;
    x_value[i] = low + incr*(i-1);
    f_value[i] = (1/sqrt(2*pi))*exp(-x_value[i]*x_value[i]/2);
```

# Chapter 10: Macro Programming 359

# Display 10.5 (continued)

```
if i=1 or i=&npts then trapsum = trapsum + f_value[i]/2;
else trapsum = trapsum + f_value[i];
end;
area_est = trapsum*incr;
output;
put;
put "est. P(&LOW < Z < &HIGH) =" area_est " (based on &NPTS points)";
put;
run;
ods rtf bodytitle file = "C:\Users\baileraJ.IT\Desktop\trap.rtf";
proc printtrapper;
title "Trapezoidal Rule Area Estimate for P(&LOW<Z<&HIGH)";
title2 "(based on &NPTS equally spaced points)";
var low high incr area_est;
run;
data trapper2;
set trapper;
array x_value(&npts) x1-x&npts;
array f_value(&npts) y1-y&npts;
do ii=1 to &npts;
xout = x_value[ii];
yout = f_value[ii];
output;
end;
run;
proc print data=trapper2;
title "Interpolation Points for Trapezoidal Rule";
var ii low high incr area_est xout yout;
run;
ods graphics on;
proc sgplot data=trapper2;
title "Plot of function values vs. x-values";
scatter x=xout y=yout;
run;
ods graphics off;
ods rtf close;
```

When you run this program, you generate the estimate of the area between -1.645 and 1.645 under a standard normal curve.

# Display 10.6 PROC PRINT output with the numerical integral of P(-1.645<Z<1.645)

# Trapezoidal Rule Area Estimate for P(-1.645<Z<1.645)
(based on 50 equally spaced points)

| Obs | low | high | incr | area_est |
| --- | --- | --- | --- | --- |
| 1 | -1.645 | 1.645 | 0.067143 | 0.89990 |

If you repeatedly run this program and change &npts to different values, then you get the output in Display 10.7.

# Display 10.7 Output written to the file est.out

```
est. P(-1.645 < Z < 1.645) -0.8999027424 (based on 50 points)
est. P(-1.645 < Z < 1.645) -0.8994989035 (based on 25 points)
est. P(-1.645 < Z < 1.645) -0.8984685898 (based on 15 points)
est. P(-1.645 < Z < 1.645) -0.8808617859 (based on 5 points)
est. P(-1.645 < Z < 1.645) -0.8258773355 (based on 3 points)
```

Display 10.7 is generated by five distinct SAS code submissions. Each submission involves reassigning a value of &npts. It would be great to loop over a range of &npts values as part of this code. SAS macro programming enables you to do this using the macro statements %DO and %END (equivalents of the DATA step statements DO-END).

## 10.5 Conditional Execution, Looping, and Macros

The %LET macro statement can be used anywhere in a program in open code. Other macro statements, such as %DO and %END and %IF and %THEN, can be used only in the context of a defined macro. A macro is a collection of commands that are evaluated by the macro processor. The general construction of a macro involves declaring the macro and any variables that might be passed to it, specifying the statements that are to be invoked in the macro, and closing with a statement that indicates the end of the macro. A macro program looks like the following:

```
%macro prog-name;
<text line1
<text line2
<text line3>
<...>
%mend prog-name;
```
