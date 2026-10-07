166 Learning SAS as Example: A Programmer's Guide, Second Edition

Figure 11.3: Listing of Data Set Three_Large

| Listing of Data Set Three_Large |
| Q1 | Q2 | Q3 | Q4 | Q5 | Q6 | Q7 | Q8 | Q9 | Q10 | SumThree |
|---|---|---|---|---|---|---|---|---|---|---|n| 001 | 4 | 1 | 3 | 9 | 1 | 2 | 3 | 5 | | 3 | 18 |
| 002 | 3 | 5 | 4 | 2 | | | | 2 | 4 | | 13 |
| 003 | 9 | 8 | 7 | 6 | 5 | | 4 | 3 | 2 | 1 | 24 |

Are you surprised to know that SAS also has a SMALLEST(1, variable-list) which gives you the smallest nonmissing value in a list of values (equal to the result of the MIN function); SMALLEST(2, variable-list) gives you the second smallest value, and so on.

# 11.6 Computing Sums within an Observation

One way to compute the sum of several variables is to write a statement such as this:

```
SumCost = Cost1 + Cost2 + Cost3;
```

What if one of the Cost values is missing? This causes the sum to be missing. If you want to ignore missing values, you can either write some DATA step logic, or simply use the SUM function, like this:

```
SumCost = sum(of Cost1-Cost3);
```

If one or two of the Cost values are missing, the SUM function returns a missing value. If you want the sum to be 0 if all the Cost arguments are missing, a neat trick is to include a 0 in the list of arguments, like this:

```
SumCost = sum(0, of Cost1-Cost3);
```

You can also see how useful the SUM function is when you have a large number of variables to sum. Here is an example.

You have a SAS data set (EndOfYear) containing Pay-Pay12 and Extra-Extra12. You want to compute the sum of these 24 values. In addition, you want the sum to be 0 if all 24 values are missing. Here is the program:

# Program 11.6: Using the SUM Function to Compute Totals

```
data Sum;
  set Learn.EndOfYear;
  Total = sum(0, of Pay-Pay12, of Extra-Extra12);
run;
```