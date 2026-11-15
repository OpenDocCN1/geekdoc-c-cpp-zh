# PRACTICE!

Give the preprocessor directives to assign symbolic constants for these constants:

+   1. Speed of light, c = 2.99792 × 10^8 m/s
+   2. Charge of an electron, e = 1.602177 × 10^-19 C
+   3. Avogadro's number, N_A = 6.022 × 10^23 mol^-1
+   4. Acceleration of gravity, g = 9.8 m/s^2
+   5. Acceleration of gravity, g = 32 ft/s^2
+   6. Mass of the Earth, M_E = 5.98 × 10^24 kg
+   7. Radius of the Moon, r = 1.74 × 10^6 m
+   8. Unit of length, Unit_Length = 'm'
+   9. Unit of time, Unit_Length = 's'

# 2.3 Assignment Statements

Assignment statement An assignment statement is used to assign a value to an identifier. The general form of the assignment statement is

```
identifier = expression;
```

Expression where an expression can be a constant, another variable, or the result of an operation. Consider the following two sets of statements that declare and give values to the variables sum, x1, and ch:

```
double sum=10.5;
int x1=3;
char ch='a';

double sum;
int x1;
char ch;
...
sum = 10.5;
x1 = 3;
ch = 'a';
```

After either set of statements is executed, the value of sum is 10.5, the value of x1 is 3, and the value of ch is 'a', as shown in the following memory snapshot:

![](bbox=[0.43, 0.725, 0.74, 0.76])

In the previous example, the statements on the left define and initialize the variables at the same time; the assignment statements on the right could be used at any point in the program, and thus may be used to change (as opposed to initialize) the values in variables.

Multiple assignments are also allowed in C, as in the following statement, which assigns a value of zero to each of the variables x, y, and z:

```
x = y = z = 0;
```

Multiple assignments are discussed further at the end of this section.