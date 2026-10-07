# 372 Learning SAS as Example: A Programmer's Guide, Second Edition

# 21.12 More Examples of the Single Trailing @ Sign

It might be useful to show some more examples of the single trailing @. Suppose you have a raw data file containing data on males and females. Suppose that you only want to read data on females. One way would be to read all the variables of interest, including Gender, and test if Gender is equal to F. If so, keep the observation; if not, delete it.

This is very inefficient. It is better to read the Gender value, check it, and then only the remaining values if Gender is equal to F.

Let's use the Bank.txt (see the following description) for an example of how this works. Here is the file description:

| Variable | Description | Starting Column | Ending Column | Data Type |
|---|---|---|---|---|n| Subj | Subject Number | 1 | 3 | Character |
| DOB | Date of Birth | 4 | 13 | Character |
| Gender | Gender | 14 | 14 | Character |
| Balance | Bank Account Balance | 15 | 21 | Numeric |

An efficient program to read data from this file, keeping only data on females, would be as follows:

# Program 21.16: Another Example of a Trailing @ Sign

```
data Females;
  infile 'C:\books\Learning\Bank.txt' pad;
  input @14 Gender $. @;
  if Gender != 'F' then delete;
  input @1 Subj $3;
        @4 DOB mmddyyy10;
        @15 Balance 7.;
run;
```

The first INPUT statement reads a single column to determine the value of Gender. The trailing @ prevents SAS from going to a new line. Next, if the value is not F, the DELETE statement instructs SAS not to output an observation to the SAS data set and return to the top of the DATA step.

# 21.13 Creating Multiple Observations from One Line of Input

There are times you want to place data for several subjects on a single line (or someone gave you a file like this). For example, suppose you have some X,Y pairs and want to create a SAS data set. One way is to place one pair of points on each input line, like this: