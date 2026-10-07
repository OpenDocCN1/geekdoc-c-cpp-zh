# APPENDIX B

# SAS® FUNCTION REFERENCE

SAS functions can be used in a DATA statement to calculate new variables or as a part of a conditional statement. This appendix is more of a reference than a tutorial, but it does illustrate the use of a number of common functions in SAS. It is not exhaustive list of functions, but it does include commonly used functions that are useful in manipulating data in the preparation for analysis. Some examples are provided for functions, whose use may not be apparent in a simple description. For a more extensive description of this material, please refer to the SAS documentation.

# B.1 USING SAS FUNCTIONS

Here are some examples of how SAS functions are used:

```
DATA NEWDATA; SET OLDDATA;
TOTAL=SUM(A, B, C);
GENDER=UPCASE(SEX);
SQRAGE=SQRT(AGE);
RUN;
```

Note that in these cases, the function on the right side of the = sign does something to the argument(s) in the parentheses and returns a value, which is assigned to the name function on the left-hand side of the total of the = sign.

The SUM function returns the total of the variables A, B, and C. The SQRT function returns the square root of the AGE variable. The UPCASE function makes all character values in the SAS variable. For example, if the SEX variable contains the value f, then the GENDER variable will contain the value F. The syntax for a function is

```
NEWVARIABLE = FUNCTIONNAME(argument1, argument2... argumentk);
```

® Essentials: Mastering SAS for Data Analytics, Second Edition. Alan C. Elliott and Wayne A. Woodward. © 2016 John Wiley & Sons, Inc. Published 2016 by John Wiley & Sons, Inc.

472