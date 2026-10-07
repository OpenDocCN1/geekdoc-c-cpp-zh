
# Chapter 11: Working with Numeric Functions

To make the program bit easier to read, you can simulate a descending sort by listing the Quiz scores in reverse order like this:

```sas
call sort(of Quiz8 - Quiz1); /**This is a descending sort***
if n(of Quiz1-Quiz8) ge 7 then Quiz_Score = mean(of Quiz1 - Quiz6);
```

You will find many examples using CALL SORTN so you can write from a tedious program.

## 11.13 Problems

Solutions to odd-numbered problems are located at the back of this book. Solutions to all problems are available to professors. If you are a professor, visit the book's companion website at support.sas.com/cod for information about how to obtain the solutions to all problems.

- 1. Using the SAS data set, the body mass index (BMI) defined as the weight in kilograms divided by the height (meters). Create four other variables based on BMI: 1) BMIRound to the nearest integer, 2) BITenth is the BMI rounded to the nearest tenth, 3) BMIGroup is the BMI rounded to the nearest 5, and 4) BITTrunc is the BMI with a fractional amount truncated. Conversion factors you will need are: 1 Kg equals 2.2 lbs and 1 inch = .254 cm.
- 2. Count the number of missing values for WBC, RBC, and Chol in the Blood data set. Use the MISSING function to detect missing values.
- 3. Create a new, temporary SAS data set (Miss Blood) based on Gender, RBC, and Chol to a missing value if WBC is missing. Use the MISSING and CALL MISSING functions in this program.
- 4. The SAS data set Psych contains an ID variable, 10 question responses (Ques1-Ques10), and 5 scores (Score1-Score5). You want to create a new, temporary SAS data set (Evaluate) containing the following:
    - a. A variable named QuesAve computed as the mean of Ques1-Ques10. Perform this computation only if there are seven or more nonquestion values.
    - b. If there are no missing Score values, compute the minimum score (MinScore), the maximum score (MaxScore), and the second highest score (SecondHighest).
- 5. The SAS data set Psych contains an ID variable, 10 question responses (Ques1-Ques10), and 5 scores (Score1-Score5). You want to create a new, temporary SAS data set (Evaluate) containing the following:
    - a. A value (ScoreAve) consisting of the mean of the three highest Score values. If there are fewer than three nonscoring values, ScoreAve should be missing.
    - b. An average of Ques1-Ques10 (call it QuesAve) if there are seven or more nonmissing values.
    - c. A composite score (Composite) equal to ScoreAve plus 10 times QuesAve.
- 6. Write a short DATA_NULL step to determine the largest integer you can score on your computer in 3, 4, 5, 6, and 7 bytes.
- 7. Given values of x, y, and z, compute the following (using a DATA_NULL step):
    - d. AbsZ = absolute value of z
    - e. Expp = e raised to the x power
    - f. Circumference = 2 times pi times y
    Use values of x, y, and equal to 10, 20, and -30, respectively. Round the values for b and c to the nearest .001.
- 8. Create a temporary SAS data set (Random) containing 1,000 observations, each with a random integer from 1 to 5. Make that all integers in the range are equally likely. Run PROC FREQ to test this assumption.
- 9. Using the random functions, create a temporary SAS data set (Fake) with 100 observations. Each observation should contain a subject number (Subj) starting from 1, a random gender (approximately 40% females and 60% males), and a random age (integers from 1 to 50). Compute the frequencies for Gender and list the first 10 observations in the data set.
- 10. Data set Char Num contains character variables Age and Weight and numeric variables SS and Zip. Create a new, temporary SAS data set called Convert with new variables NumAge and NumWeight that are numeric values of Age and Weight, and CharSS and CharZip that are character variables from SS and Zip. CharSS should contain leading 0s and dashes in the appropriate places for Social Security numbers and CharZip should contain leading 0s.
    **Hint:** The Z5 format includes leading 0 for the ZIP code.
- 11. Repeat Problem 10, except this time use the same variable names for the converted variables.
    **Hint:** Swap and drop.
- 12. Using the Stocks data set (containing variables Date and Price), compute daily changes in the prices. Use the statements to create the plot.

```sas
title "Plot of Daily Price Differences";
proc sgplot data=Difference;
series x=Date y=Price;
run;
```
Plot the daily price in data set Stocks along with a moving average of the prices using a three-day moving average. Use the PLOT statements to produce the plots.

```sas
title "Plot of Price and Moving Average";
proc sgplot data=Moving;
series x=Date y=Price;
series x=Date y=Moving;
run;
```

## Chapter 12: Working with Character Functions

- 12.1 Introduction........................................................................................................................... 181
- 12.2 Determining the Length of a Character Value............................................................... 182
- 12.3 Changing the Case of Characters........................................................................................... 182
- 12.4 Removing Characters from Strings....................................................................................... 183
- 12.5 Joining Two or More Strings Together............................................................................... 184
- 12.6 Removing Leading or Trailing Blanks........................................................................... 185
- 12.7 Using the COMPRESS Function to Remove Characters from a String....... 186
- 12.8 Searching for Characters...................................................................................................... 189
- 12.9 Searching for Individual Characters............................................................................... 190
- 12.10 Searching for Words in a String.................................................................. 191
- 12.11 Searching for Character Classes.................................................................. 192
- 12.12 Using the NOT Functions for Data Cleaning............................................................... 193
- 12.13 Extracting Part of a String.............................................................................. 194
- 12.14 Dividing Strings into Words......................................................................... 196
- 12.15 Performing a Fuzzy Match............................................................................... 197
- 12.16 Substituting Strings or Words................................................................ 199
- 12.17 Problems............................................................................... 201

### 12.1 Introduction

This chapter covers some of the basic functions that work with character values. These functions enable you to search for characters, strings apart and put them back again, and remove characters from a string. With SAS9, you can search for or remove classes of characters, such as digits, punctuation marks, or space characters. You can even perform fuzzy matches between two values—useful in matching names that may be misspelled. For more information, see SAS Functions.

### 12.2 Determining the Length of a Character Value

The LENGTH function returns the length of a character value, not counting trailing blanks. An older function, LENGTH, performed exactly as the LENGTH function with one exception—when the argument is a missing value. The LENGTH function returns 1 in this situation—the LENGTH function returns 0 (the preferred).

For those curious readers, the ‘N’ at the end of LENGTH function stands for ‘null string,’ that is, a string of zero length. This concept was added with SAS9. You will see other functions in this chapter that are familiar to you except for that they now use an ‘N’. In most cases, use the ‘N’ version. Here is an example of the LENGTH function:

You have a SAS data set (Sales) that includes a variable Name. You want to see all the names that are longer than 12 characters. Here is the program:

#### Program 12.1: Determining the Length of a Character Value

```sas
data Long_Names;
set Learn.Sales;
if length (Name) gt 12;
run;
```

The subset IF statement is true when the number of characters in Name exceeds 12 (not counting trailing blanks including any blanks within the string).

Another function, LENTC, returns the storage length of a string. You may want to test storage lengths when you are combining data from multiple files.

### 12.3 Changing the Case of Characters

A common programming problem is matching values where the case of the two values may not be the same. Suppose you are presented with two SAS data sets: one has names in mixed case, and the other has names in uppercase. You want to merge the two data sets.

A listing of data sets Mixed and Upper are shown here.

Note: Data sets are already sorted by Name.

#### Figure 12.1: Listing of Data Sets Mixed and Upper

| Listing of Data Set Learn.Mixed | Listing of Data Set Learn.Upper |
|---|---||
| Name | ID | Name | DOB |
| Daniel Fields | 123 | DANIEL FIELDS | 01/03/1966 |
| Patrice Helms | 233 | PATRICE HELMS | 05/23/1988 |
| Thomas chien | 998 | THOMAS CHIEN | 11/12/2000 |
