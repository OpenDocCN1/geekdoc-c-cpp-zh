# Chapter 3: Reading Raw Data from External Files 39

2. You are given a CSV (comma-separated values) called Political.csv containing state, political party, and age. A listing of the file Political.txt is shown here:

```
"MJ",Ind,55
"CO",Dem,45
"NY",Rep,23
"FL",Dem,66
"NJ",Rep,34
```

+   a. Write a SAS program to create a temporary data set called Vote. Use the variable names State, Party, and Age. Age should be stored as a numeric variable; State and Party should be stored as character variables.

+   b. Include a procedure to list the observations in this data set.

+   c. Include a procedure to compute frequencies for Party.

3. You are given a text file where dollar signs were used as delimiters. To identify missing values, two dollar signs were entered. Values in this represent last name, employee number, and annual salary.

Here is a listing of the file Company.txt:

```
Roberts$$234$45000
Chien$$747777$
Walters$$75000
Rogers$$7272$78131
```

Using this data as input, create a temporary SAS data set called Company with the variables Name(character), EmpNo(character), and Salary (numeric).

4. Repeat 2 using a FILENAME statement to create a fileref instead of the INFILE statement.

5. You want to create a program that uses a DATALINES statement to read in values for X and Y. In the DATA step, you want to create a new variable, Z, equal to 10 + 50X + 2X² - 25Y + Y². Use the (X,Y) data pairs: (1,2), (3,6), (5,9), and (9,11).

6. You have a text file Bankdata.txt with that values arranged as:

| Variable | Description | Starting Column | Ending Column | Data Type |
| --- | --- | --- | --- | --- |
| Name | Name | 1 | 15 | Char |
| Acct | Account number | 16 | 20 | Char |
| Balance | Acct balance | 21 | 26 | Num |
| Rate | Interest rate | 27 | 30 | Num |

Create a temporary SAS data set called Bank using this data file. Use column input to specify the location of each value. Include in this data variable calculated Interest computed by multiplying Balance by Rate. List the contents of this data set using PROC PRINT.

Here is a listing of the text file:

```
Philip Jones V1234 4322.32
Nathan Philips V1399 15202.45
Shu Lu W8892 45123.45
Betty Boop V7677 50002.45
```

![](bbox=[0.202, 0.963, 0.282, 0.978])