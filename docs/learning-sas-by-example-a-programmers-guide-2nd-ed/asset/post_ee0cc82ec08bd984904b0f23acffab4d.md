
## 3.6 Reading Data Values Separated by Delimiters Other Than Blanks

Remember that the default delimiter for list input is a blank. Using the INFILE option DSD changes the default to a comma. What if you have a file with other delimiters, such as tabs or colons? No problem! You only need to add the DLM-option to the INFILE statement. For example, the following lines of data use colons as delimiters.

Example of a file using colon delimiters:

```
M:50:68:155
F:23:60:101
M:65:72:220
F:35:65:133
M:15:71:166
```

To read this file, you could use this INFILE statement:

```
infile 'file-description' dlm=';';
```

You can spell out the name of the DELIMITER=option instead of using the abbreviation DLM if you like, for example:

```
infile 'file-description' delimiter=';';
```

You can use the DSD and DLM-options together. This combination of options performs all the actions requested by the DSD option (see Section 3.4) and overrides the default DSD delimiter (comma) with a delimiter of your choice.

```
infile 'file-description' dsd dlm=';';
```

Tabs present a particularly interesting problem. What character do you place between the quotes on the DLM-option? You cannot click the TAB key. Instead, you need to represent the tab by its hexadecimal equivalent. For ASCII files (the coding method used on Windows platforms and UNIX operating systems—it stands for American Standard Code for Information Interchange), you would use the following:

```
infile 'file-description' dlm='09x';
```

For EBCDIC files (used on most mainframe computers—it stands for Extended Binary-Coded Decimal Interchange Code), you would use the following statement:

```
infile 'file-description' dlm='05x';
```

> Note: These two values are hexadecimal constants. If you know (or look up) the hexadecimal value of any character, you can represent it in a SAS statement by placing the hexadecimal value in single or double quotes and following the value immediately (no space) by an upper- or lowercase x.

## 3.7 Placing Data Lines Directly in Your Program (the DATALINES Statement)

Suppose you want to write a short test program in SAS. Instead of having your data in an external file, you can place your lines of data directly in your SAS program using a DATALINES statement. For example, if you want to read data from the text file Mydata.txt (blank delimited data with values for Gender, Age, Height, and don't want to go through the trouble of wrangling the external file, you could use Program 3.4.

### Program 3.4: Demonstrating the DATALINES Statement

```
data demographic;
  input Gender $ Age Height Weight;
datalines;
  M 50 68 155
  F 23 60 101
  M 65 72 220
  F 35 65 133
  M 15 71 166
```

As you can see from this example, the INFILE statement was removed and a DATALINES statement was added. Following DATALINES are your lines of data. Finally, a semicolon is used to end the DATA step. The lines of data must be the last element in the DATA step—any other statements must come before the lines of data.

While you would probably not use DATALINES in a real application, it is extremely useful when you want to write short test programs.

As a historical note, the DATALINES statement used to be called the CARDS statement. If you don't know what a computer card is, ask an old person. By the way, you can still use the CARDS in place of DATALINES if you want.

## 3.8 Specifying INFILE Options with the DATALINES Statement

What if you use DATALINES and want to use one or more of the INFILE options, such as DLM=DSD? You can use many of the INFILE options with DATALINES by using a reserved file reference called. For example, if you wanted to run Program 3.2 without an external file, you could use Program 3.5.

### Program 3.5: Using INFILE Options with DATALINES

```
data Demographics;
  infile datas dsd;
  input Gender $ Age Height Weight;
datalines;
  "M",50,68,155
  "F",23,60,101
  "M",65,72,220
  "F",35,65,133
  "M",15,71,166
```

## 3.9 Reading Raw Data from Fixed Columns — Method 1: Column Input

Many raw data files store information in fixed columns. This has several advantages over data values separated by delimiters. First, you don't have to worry about missing values. If you do not have a value, you can choose the appropriate columns blank. Next, when you write your INPUT statement, you can choose variables to read and in what order to read them.

The simplest method for reading data in fixed columns is called column input. This method of input can read character data and standard numeric values. By standard numeric values, we mean positive or negative numbers as well as numbers in exponential format (for example, 3.4E3 means 3.4 times 10 to the power 3). This form of input cannot handle values with commas or dollar signs. You can only read dates as character values with this form of input. For for example

You have a raw data file called bank.txt in a folder C:\books\learning on your Windows computer. A data description for this file follows:

| Variable | Description | Starting Column | Ending Column | Data Type |
| --- | --- | --- | --- | --- |
| Subj | Subject Number | 1 | 3 | Character |
| DOB | Date of Birth | 4 | 13 | Character |
| Gender | Gender | 14 | 14 | Character |
| Balance | Bank Account Balance | 15 | 21 | Numeric |

File C:\books\learning\Bank.txt

```
1                2
00110/21/1955M 1145
00211/18/2001F 18722
00305/07/1944M 123.45
00407/25/1945F -12345
<- Columns (not part of the file)
```

Program 3.6 is a SAS program that reads data values from this file.

### Program 3.6: Demonstrating Column Input

```
data Financial;
  infile 'C:\books\learning\Bank.txt';
  input Subj      $1-3
        DOB       $4-13
        Gender    $14-14
        Balance   15-21;

run;

title "Listing of Financial";
proc print data=Financial;
run;
```

You specify a variable name, a dollar sign if the variable is a character value, the starting column, and the ending column (if the value takes more than one column). In this program, the number of columns you specify for each character variable determines the number of bytes SAS uses to store these values; for numeric variables, SAS will always use 8 bytes to store these values, regardless of how you specify.

32 Learning SAS by Example: A Programmer’s Guide, Second Edition

## 3.10 Reading Raw Data from Fixed Columns — Method 2: Formatted Input

Formatted input also reads data from fixed columns. It can read both character and standard numeric data as well as nonstandard numeric values, such as numbers with dollar signs, and commas in a variety of formats. Formatted input is the most common and powerful of all the input methods. Anytime you have nonstandard data in fixed columns, you should consider using formatted input to read the file.

Let’s start with the same raw data file (Bank. txt) that was used in Program 3.6. First examine the program, and then read the explanation.
