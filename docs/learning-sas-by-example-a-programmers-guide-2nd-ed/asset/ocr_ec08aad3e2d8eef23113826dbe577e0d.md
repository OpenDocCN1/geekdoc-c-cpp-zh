# Chapter 7: Performing Conditional Processing 89

There are several ways to prevent your missing values from being included in AgeGroup 1. Here are
options:

```
if Age lt 20 and Age ne . then AgeGroup = 1;
if Age ge 0 and Age lt 20 then AgeGroup = 1;
if 0 le Age lt 20 then AgeGroup = 1;
if Age lt 20 and not missing (Age) then AgeGroup = 1;
```

All of these statements result in the correct value for AgeGroup. Subjects with a missing value for Age will also have a missing value for AgeGroup.

The first IF statement uses the fact to refer to a numeric missing value in a DATA step by a period. The last IF statement uses the MISSING function. This function returns TRUE if the argument (the variable in parentheses) is missing, and FALSE if the argument is not missing. The MISSING function also works with character data.

This program can be improved. If a person is less than 20 years of age, the first IF statement and AgeGroup is set to 1. All the remaining IF statements are still executed (although they will be false and AgeGroup remains 1). A better way to write this program is to change all the IF statements after the first one to ELSE IF statements.

Here is what the corrected program looks like:

# Program 7.2: Corrected Program to Group Ages into Age Groups

```
data Conditional;
  length Gender $ 1
  Quiz $ 2;
  input Age Gender Midterm Quiz FinalExam;
  if Age lt 20 and not missing (age) then AgeGroup = 1;
  else if Age ge 20 and Age lt 40 then AgeGroup = 2;
  else if Age ge 40 and Age lt 60 then AgeGroup = 3;
  else if Age ge 60 then AgeGroup = 4;
datalines;
```

Using this logic, when any of the IF statements is true, the following ELSE statements are not evaluated.

An alternative way to write this program is to test for a missing value in the first IF statement and use the ELSE statements to advance, as follows:

# Program 7.3: An Alternative to Program 7.2

```
data Conditional;
  length Gender $ 1
  Quiz $ 2;
  input Age Gender Midterm Quiz FinalExam;
  if missing (Age) then AgeGroup = .;
  else if Age lt 20 then AgeGroup = 1;
  else if Age lt 40 then AgeGroup = 2;
  else if Age lt 60 then AgeGroup = 3;
  else if Age ge 60 then AgeGroup = 4;
datalines;
```