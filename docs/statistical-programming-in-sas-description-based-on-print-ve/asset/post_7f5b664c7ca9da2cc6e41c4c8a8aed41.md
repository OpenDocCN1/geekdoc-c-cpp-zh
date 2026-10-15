
### Display 8.22 Defining indicator variables for literacy categories

```
data toyexample;
    input literacy @@;

/* method 1-2:
    Boolean trick to assign category labels 1-4;
    If a logical comparison is TRUE (FALSE), it evaluates to 1 (0)
    e.g. if literacy=54, (53<literacy<=76)=TRUE while
        (0<literacy<=53)=(76<literacy<=90)=(90<literacy<=100)=FALSE
        And so cat_literacy1 = 1*0 + 2*1 + 3*0 + 4*0 = 2
*/

cat_literacy1 = 1*(0<literacy<=53) + 2*(53<literacy<=76)
    + 3*(76<literacy<=90) + 4*(90<literacy<=100);

cat_literacy2 = 1*(literacy<=53) + 2*(53<literacy<=76)
    + 3*(76<literacy<=90) + 4*(90<literacy<=100);

/*
    method 3:
    First check for nonmissing and valid ranges before Boolean trick
*/

if ( (literacy NE .) AND (0<=literacy<=100) ) then
    cat_literacy3 = 1*(literacy<=53) + 2*(53<literacy<=76)
        + 3*(76<literacy<=90) + 4*(90<literacy<=100);

/* method 4:
    IF-THEN-ELSE blocks to assign category labels
*/

if ( (literacy EQ .) OR (100<literacy)
        OR (literacy<0) ) then cat_literacy4=.;
else if (literacy <=53) then cat_literacy4=1;
else if (literacy <=76) then cat_literacy4=2;
else if (literacy <=90) then cat_literacy4=3;
else cat_literacy4=4;
datalines;
-99 25.55 73.7 83   99.9 107 .
;
run;
ods rtf file="C:\Users\baileraj.IT\Desktop\Display-8-22.rtf";
proc print data=toyexample;
run;
ods rtf close;
```

The four different indicator variables are shown in Display 8.23.

### Display 8.23 Output from PROC PRINT for the different indicator variables

| Obs | literacy | cat_literacy1 | cat_literacy2 | cat_literacy3 | cat_literacy4 |
|---|---|---|---|---|---|
| 1 | -99.00 | 0 | 1 | . | . |
| 2 | 25.55 | 1 | 1 | 1 | 1 |
| 3 | 73.70 | 2 | 2 | 2 | 2 |
| 4 | 83.00 | 3 | 3 | 3 | 3 |
| 5 | 99.90 | 4 | 4 | 4 | 4 |
| 6 | 107.00 | 0 | 0 | . | . |
| 7 | . | 0 | 1 | . | . |

Look at the first method that defines the variable `cat_literacy1`. When literacy=54, the first condition (0<literacy<=53) is FALSE. The second condition (53<literacy<=76) is TRUE. The third condition (76<literacy<=90) is FALSE. The fourth condition (90<literacy<=100) is FALSE. Consider the following expression:

```
cat_literacy1 = 1*(0<literacy<=53) + 2*(53<literacy<=76)
              + 3*(76<literacy<=90) + 4*(90<literacy<=100);
```

If TRUE =1 and FALSE =0, this expression evaluates to the following:

```
cat_literacy1 = 1*(0) + 2*(1) + 3*(0) + 4*(0) = 2
```

If you want the missing values of LITERACY preserved, or if you want values outside of the valid range to be assigned missing values, then this code does not behave as expected. If LITERACY is missing (.), or if it has a value outside of the range that is tested (-99 to 107), then none of the conditions are TRUE and `cat_literacy1=0`.

The second method leads to other behavior worth noting. Consider the following expression:

```
cat_literacy2 = 1*(literacy<=53) + 2*(53<literacy<=76)
              + 3*(76<literacy<=90) + 4*(90<literacy<=100);
```

This method assigns `cat_literacy2=1` if LITERACY is -99 or missing. This assignment occurs because condition (literacy<=53) is TRUE for -99 (no surprise because -99≤53), and missing observations are TRUE (possibly a surprise because you might not know that missing (.)≤53).

The third and fourth methods behave as expected. An IF check for nonmissing values and a valid range is conducted first. If the value passes this check, then the categories are assigned following the first two methods of assigning a category. The fourth method uses an IF–THEN–ELSE construct. The code is a bit longer, but it might be easier for you to understand. The bottom line is always test your code with boundary, invalid, and missing cases to make sure that you get what you want.

## 8.4 Ordering How Tasks Are Done

Before you start implementing programming solutions for problems, you need to know the order in which calculations are executed (the so-called order of operations or precedence of operations). Let’s take a quick look at a common source of headaches for beginning programmers. (If you already know this stuff, then skip ahead.) Computers do what you say, not what you mean. Thus, you should carefully code programs in general and code equations in particular. When coding an equation, remember that computers execute the parts of the equation in a particular order. If there are no parentheses, exponentiation is done first. Then, multiplication and division (equal precedence) are done second. And, addition and subtraction (equal precedence) are done last. Expressions in parentheses are processed before other expressions are processed. Evaluation occurs from left to right when processing an equation. AND operators are executed before OR operators, which can make a difference in complicated expressions when programs do not include parentheses.

Let’s move from the abstract to the concrete. The next example illustrates some of the dangers of careless coding. In the example, pay special attention to the pairs of calculations:

```
x1a=3×2² versus x1b=(3×2)²
x2a=3−2/2 versus x2b=(3−2)/2
x3a=−2² versus x3b=(−2)²
```

You probably expect the pairs to yield different values because of the grouping imposed by the parentheses. However, this is not quite as clear when you look at the code. For example, if you naively thought that code is processed from left to right without considering the order of operations, then you might expect `x2a=3−2/2` and `x2b=(3−2)/2` to yield the same answer. Display 8.24 includes test code that demonstrates that this is not the case.

### Display 8.24 Test code for order of operations

```
data preced_test;
  x1a = 3*2**2;
  x1b = (3*2)**2;
  x2a = 3-2/2;
  x2b = (3-2)/2;
  x3a = -2**2;
  x3b = (-2)**2;
  put '--------------------------------';
  put ' | Order of operations |';
  put ' | illustrated |';
  put '--------------------------------';
  put '  3*2**2 = ' x1a;
  put ' (3*2)**2 = ' x1b;
  put '  3-2/2 = ' x2a;
  put ' (3-2)/2 = ' x2b;
  put '  -2**2 = ' x3a;
  put ' (-2)**2 = ' x3b;
run;
```

The result of each operation coded in Display 8.24 is shown in Display 8.25.

### Display 8.25 Output from the test code for the order of operations

```
--------------------------------
| Order of operations |
| illustrated |
--------------------------------
  3*2**2 = 12
 (3*2)**2 = 36
  3-2/2 = 2
 (3-2)/2 = 0.5
  -2**2 = -4
 (-2)**2 = 4
```

There is a simple moral to this programming story—use parentheses if you want operations to be conducted in a specific order.

## 8.5 What Goes and What Stays in a Data Set

You have used DATA steps to read data into variables and to manipulate data such as defining new variables. After you have finished these tasks, you might want to simplify the data set by getting rid of extraneous variables. The options DROP and KEEP specify variables to be eliminated from or saved in a SAS data set. In addition to eliminating variables, you might want to keep observations that satisfy some criteria. The statements WHERE and IF enable you to specify values of variables that you want to keep in a SAS data set. For example, the following statement includes only observations of the numeric variable LITERACY that have missing values:

```
if literacy EQ .;
```

The IF statement can be used in a series of IF-THEN-ELSE expressions. The WHERE statement can do a similar job to the IF statement, but it has specific operators, BETWEEN-AND, CONTAINS, IS NULL, IS MISSING, LIKE, and SAME-AND, which are documented extensively in SAS Help.

Programming statements in DATA steps are often needed for even routine analyses. In Chapter 2, the SET statement placed the contents of multiple data sets into a newly created data set. The OUTPUT statement wrote a current specification of a collection of variables to a data set. The OUTPUT statement can be used to expand a data set so that multiple lines are created in the new data set for each observation in the current data set. This is demonstrated in Display 8.26, which illustrates the manipulation of variables and records. The code starts by reading the nitrofen data into a SAS data set named nitro. The contents of nitro are then set into the new SAS data set `nitrofenA`. A single record for each animal is expanded into separate lines for each brood. The data for the first four animals are printed by imposing a WHERE restriction. Informal challenge: Can you think of an alternative way of incorporating this same print restriction? This type of data structure is commonly used for particular models in SAS such as the linear mixed effects model, which can be analyzed using PROC MIXED.
