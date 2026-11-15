In this chapter, we covered the use of conditions and if statements to select the proper statements to be executed. We also presented techniques for repeating sets of statements in loops. These loops can be implemented as while loops or for loops. Selection and repetition structures are used in most programs. In addition, we included the statements necessary to read information from a data file so that we could use the information in the program. We also presented the statements to generate a data file from a program. Data files are commonly used in solving engineering problems; therefore, this concept was presented early in the text so that we could use it in many of the later problem solutions. Finally, we covered the concept of generating a linear model for a set of data points and included the equations for determining the best fit line in terms of least squares.

# KEY TERMS

+   case label
+   case structure
+   compound statement
+   condition
+   conditional operator
+   controlling expression
+   data file
+   default label
+   divide and conquer
+   empty statement
+   end-of-file indicator
+   error condition
+   file open mode
+   file pointer
+   flowchart
+   for loop
+   iteration
+   least squares
+   linear modeling
+   linear regression
+   logical operator
+   loop
+   loop control variable
+   program walkthrough
+   pseudocode
+   relational operator
+   repetition
+   selection
+   sequence
+   sentinel signal
+   stepwise refinement
+   structured program
+   summation notation
+   test data
+   top-down design
+   trailer signal
+   validation and verification
+   while loop

# C STATEMENT SUMMARY

Declaration for file pointer:

```
FILE *sensor;
```

if statement:

```
if (temp > 100)
    printf("Temperature exceeds limit \n");
```

```
temps>100 ? printf("Caution \n"): printf("Normal \n");
```

if/else statement:

```
if (d <= 30)
    velocity = 4.25 + 0.00175*d*d;
else
    velocity = 0.65 + 0.12*d - 0.0025*d*d;
```