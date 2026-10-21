used in the expression must be assigned values before evaluation is attempted. Examples of evaluation statements are

```
x = a*b-c;
y = b/c*a;
z = a-b/c+d;
```

The blank space around an operator is optional and is added only to improve readability. When these statements are used in a program, the variables a, b, c and d must be declared and assigned values before they are used in the expressions. Similarly, the variables x, y and z must have been declared earlier for their types.

# 5.12 PRECEDENCE OF ARITHMETIC OPERATORS

An arithmetic expression without any parentheses will be evaluated from left to right using the rules of precedence of operators. There are two distinct priority levels of arithmetic operators in C#:

+   High priority  * / %
+   Low priority  + -

The basic evaluation procedure includes two left-to-right passes through the expression. During the first pass, the high priority operators (if any) are applied as they are encountered. During the second pass, the low priority operators (if any) are applied as they are encountered. Consider the following evaluation statement:

```
x = a-b/3+c*2-1
```

When a = 9, b = 12, and c = 3, the statement becomes

```
x = 9-12/3+3*2-1
```

and is evaluated as follows:

First pass

+   Step1: x = 9-4+3*2-1    (12/3 evaluated)
+   Step2: x = 9-4+6-1    (3*2 evaluated)

Second pass

+   Step3: x = 5+6-1    (9-4 evaluated)
+   Step4: x = 11-1    (5+6 evaluated)
+   Step5: x = 10    (11-1 evaluated)

However, the order of evaluation can be changed by introducing parentheses into an expression. Consider the same expression with parentheses as shown below:

```
9-12/(3+3)*(2-1)
```

Whenever the parentheses are used, the expressions within parentheses assume highest priority. If two or more sets of parentheses appear one after another as shown above, the expression contained in the left-most set is evaluated first and the right-most in the last. Given below are the new steps.

First pass

+   Step1: 9-12/6*(2-1)
+   Step2: 9-12/6*1

Second pass

+   Step3: 9-2*1
+   Step4: 9-2

Third pass

+   Step5: 7

This time, the procedure consists of three left-to-right passes. However, the number of evaluation steps remain the same as 5 (i.e., equal to the number of arithmetic operators).