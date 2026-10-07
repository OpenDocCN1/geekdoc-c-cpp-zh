If you do not supply a select-expression, each WHEN statement is evaluated to determine if the when-expression is true or false. As an example, here is Program 7.5, rewritten with a SELECT statement:

# Program 7.5: Demonstrating a SELECT Statement When a Select-Expression is Missing

```
data Conditional;
  length Gender $ 1;
  Quiz $ 2;
  input Age Gender Midterm Quiz FinalExam;
select;
  when (missing(Age)) AgeGroup = ;
  when (Age lt 20) AgeGroup = 1;
  when (Age lt 40) AgeGroup = 2;
  when (Age lt 60) AgeGroup = 3;
  when (Age ge 60) AgeGroup = 4;
  otherwise;
datalines;
```

Note that there is no select-expression in this SELECT statement. Each when-expression is evaluated, if true, the statement following the expression is executed.

# 7.6 Using Boolean Logic (AND, OR, and NOT Operators)

You can combine logical operators (also known as Boolean operators) to form fairly complex statements. As example, the data set contains information on clinic, diagnosis (DX), and weight. A program to list all patients who were seen at the HMC clinic and had either a diagnosis of 7 or 9 weighted over 180 pounds demonstrates how to combine various Boolean operators:

# Program 7.6: Combining Various Boolean Operators

```
title "Example of Boolean Expressions";
proc print data=Learn.Medical;
  where clinic 'HMC' and
  (DX in ('7','9') or
  Weight gt 180);
  id Patno;
  var Patno Clinic DX Weight VisitDate;
run;
```

Note the parentheses around the two statements separated by OR. The AND operator has precedence before the OR operator. That is, a statement such as the following:

if X and Y or Z;

is the same as this one:

if (X and Y) or Z;

If you want to perform the OR operation before the AND operation, use parentheses, like this:

if X and (Y or Z);