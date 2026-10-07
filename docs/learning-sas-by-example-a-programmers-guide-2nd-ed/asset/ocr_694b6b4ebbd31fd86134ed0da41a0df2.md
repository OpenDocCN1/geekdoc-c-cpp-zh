# Learning SAS by Example: A Programmer'ss Guide, Second Edition

critical either, though it is useful for legitimacy. It is a common practice to start each SAS statement on a new line and to indent each statement by DATA or PROC step by several spaces (author likes three spaces).

# Program 1.2: An Alternative Version of Program 1.1

```
data Veg; infile "C:\books\learning\Veggies.txt"; input
Name $ Code Days Number
Price; CostPerSeed =
/
Number;
run;
```

Another thing to note about this program is that SAS is not case-sensitive. Well, this is almost true. Of course references to external files must match the rules of your particular operating system. So, if you are running SAS under UNIX or Linux, file names will be case-sensitive. As you will see later, you get to name the variables in Program 1.1 are Name, Code, Days, Number, Price, and CostSeed. Although SAS doesn’t care whether you write these names in uppercase, lowercase, or mixed case, it will “remember” the case of each variable the first time it encounters it and uses that form of the variable name when producing reports.

# 1.4 SAS Names

SAS names follow a simple naming rule: All SAS variable names and data set names can be no longer than 32 characters and must begin with a letter or the underscore (_) character. The remaining characters in the name may be letters, digits, or the underscore character. Characters such as dashes and spaces are not allowed. Here are some valid and invalid SAS names.

| Valid SAS Names |
|---|
| Parts |
| LastName |
| First_Name |
| Ques5 |
| Cost per Pound |
| DATE |
| time |
| X12Y34Z56 |

| Invalid SAS Names |
|---|---|
| 8_enough | Begins with a number |

| | |
|---|---|
| Price per Pound | Contains blanks |
| |
| Month-total | Contains an invalid character ( - ) |
| Num% | Contains an invalid character (%) |