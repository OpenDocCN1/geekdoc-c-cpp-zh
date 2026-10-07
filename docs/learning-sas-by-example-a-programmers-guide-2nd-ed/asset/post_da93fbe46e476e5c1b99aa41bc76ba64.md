
## Program 1.1: A Sample SAS Program

SAS Program to read the Veggie.txt data file and to produce several reports;

```
options nonumber nodate;
data Veg;
infile "C:\books\learning\Veggies.txt";ninput Name $ Code $ Days Number Price;
CostPerSeed = Price / Number;
run;
```

```
title "List of the Raw Data";
proc print data=Veg;
run;
```

```
title "Frequency Distribution of Vegetable Names";
proc freq data=Veg;
tables Name;
run;
```

```
title "Average Cost of Seeds";
proc means data=Veg;
var Price Days;
run;
```

At this point in the book, we won't explain every line of the program—we'll just give an overview.

SAS programs often contain DATA steps and PROC steps. DATA steps are parts of the program where you can read or write the data, manipulate the data, and perform calculations. PROC (short for procedure) steps are parts of your program where you ask SAS to one or more of its procedures to produce reports, summarize the data, generate graphs, and much more. DATA steps begin with the word DATA and PROC steps begin with the word PROC end with a RUN statement (more on this latter). SAS processes each DATA or PROC step completely and goes on to the next step.

SAS also has global statements that affect the entire SAS environment and remain in effect from DATA or PROC step to another. In the program, the OPTIONS and TITLE statements are examples of global statements. It is important to keep in mind that the actions of global statements remain in effect until they are changed by another global statement or until you end your SAS session.

All SAS programs, whether part of DATA or PROC steps, are made up of statements. Here is the rule: all SAS statements end with semicolons.

> Note: This is an important rule if you leave a semicolon where one is needed, the program may not run correctly, resulting in hard-to-interpret error messages.

Let's discuss some of the basic rules of SAS statements. First, they can begin in any column and span several lines, if necessary. Because a semicolon determines the end of a SAS statement, you can place more than one statement on a single line (although this is not recommended as a matter of style).

To make this clear, let's look at some of the statements in Program 1.1.

You could write the DATA step as shown in Program 1.2. Although this program is identical to the original, notice that it doesn't look organized, making it hard to read. Notice, also, spacing is not critical either, though it is useful for legitimacy. It is a common practice to start each SAS statement on a new line and to indent each statement by DATA or PROC step by several spaces (author likes three spaces).

## Program 1.2: An Alternative Version of Program 1.1

```
data Veg; infile "C:\books\learning\Veggies.txt"; input
Name $ Code Days Number
Price; CostPerSeed =
/Number;
run;
```

Another thing to note about this program is that SAS is not case-sensitive. Well, this is almost true. Of course references to external files must match the rules of your particular operating system. So, if you are running SAS under UNIX or Linux, file names will be case-sensitive. As you will see later, you get to name the variables in Program 1.1 are Name, Code, Days, Number, Price, and CostSeed. Although SAS doesn’t care whether you write these names in uppercase, lowercase, or mixed case, it will “remember” the case of each variable the first time it encounters it and uses that form of the variable name when producing reports.

## 1.4 SAS Names

SAS names follow a simple naming rule: All SAS variable names and data set names can be no longer than 32 characters and must begin with a letter or the underscore (_) character. The remaining characters in the name may be letters, digits, or the underscore character. Characters such as dashes and spaces are not allowed. Here are some valid and invalid SAS names.

| Valid SAS Names |
| :--- |
| Parts |
| LastName |
| First_Name |
| Ques5 |
| Cost per Pound |
| DATE |
| time |
| X12Y34Z56 |

| Invalid SAS Names | Reason |
| :--- | :--- |
| 8_enough | Begins with a number |
| Price per Pound | Contains blanks |
| Month-total | Contains an invalid character ( - ) |
| Num% | Contains an invalid character (%) |

## 1.5 SAS Data Sets SAS Data Types

We will talk about SAS data sets throughout this book. Now, you need to know that when SAS reads data from anywhere (for example, raw data or spreadsheets), it stores the data in its own special form called a SAS data set. Only SAS can read and write SAS data sets. If you opened a SAS data set with another program (Microsoft Word, for example), it would not be a pretty sight—it would consist of recognizable characters and many funny-looking graphics. In other words, it would look like nonsense. Even if SAS is reading data from an Oracle table or DB2, it is actually converting the data into a SAS data set in the background.

The good news is you don't ever have to worry about how SAS is storing its data or the structure of a data set. However, it is important to understand that SAS data sets contain two parts: a descriptor and a data portion. Not only does SAS store the actual values for you, it stores information about these values (like storage lengths, labels, and formats). We will discuss this much later.

SAS data sets have only two types of variables: character and numeric. This makes it much simpler to use and understand than other programs that have more types of data (for example, integer, and logic).). SAS determines a fixed storage length for every variable. SAS users never need to think about storage lengths for numerical values—they are stored in 8 bytes (or 14 or 15 digits, depending on your operating system) if you don't specify otherwise. The majority of SAS users will never have to change this default value (it can lead to complications and only be considered by experienced SAS programmers). Each character value (data stored as letters, special characters, and digits) is assigned a fixed length explicitly by program statements or by various rules that SAS has about the length of character variables.

## 1.6 The SAS Windows Environment, SAS Enterprise Guide, and the SAS University Edition

Because SAS runs on many different platforms (mainframes, microcomputers running various operating systems, UNIX, and Linux), the way you write and run programs vary. You might use a general-purpose text editor on a mainframe to write a SAS program, submit it, and send the output back to a file. In PCs, you use the SAS environment, where you write your program in the Editor (window), see any error messages and comments about your program in the Log window, and view your output in the Output window. Other ways to submit SAS programs are through called Enterprise Guide, which is a menu-driven system that allows you to write SAS programs and produce reports. The SAS University Edition (free) uses SAS as its entry into the SAS system. There are many excellent books published by SAS that offer detailed instructions on how to run SAS programs on each platform. This book concentrates on how to write SAS programs. You will find that SAS programs, regardless of what computer or operating system you are using, look basically the same. Typically, the only changes you need to make migrate SAS program from one platform to another is the way you describe external sources and where you store SAS programs and output.

## 1.7 Problems

Solutions to odd-numbered problems are located at the back of this book. Solutions to all problems are available to professors. If you are a professor, visit the book's companion website at support.sas.com/cody for information about how to obtain the solutions to all problems.

- 1. Identify which of the following variable names are valid SAS names:
- Height
- HeightInCentimeters
- Height_in_centimeters
- Wt-kg
- hyphens-in-name-x123y456
- 76Trombones
- MiXeDeCase

- 2. In the following list, classify each data set name as valid or invalid:
- Clinic
- clinic
- work
- hyphens-in-the-name
- 123GO
- Demographics_2006

- 3. You have a data set consisting of Student_ID, English, History, Math, and Science_Scores on 10 students.
- a) The number of variables is _________
- b) The number of observations is _________

- 4. True or false:
- a) You can place more than one SAS statement on a single line.
- b) You can use several lines for a single SAS statement.
- c) SAS has three data types: character, numeric, and integer.
- d) OPTIONS and TITLE statements are considered global statements.

- 5. What is the default storage length for SAS numeric variables (in bytes)?
