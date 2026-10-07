# Program 1.1: A Sample SAS Program

*SAS Program to read the Veggie.txt data file and to produce several reports;

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

You could write the DATA step as shown in Program 1.2. Although this program is identical to the original, notice that it doesn't look organized, making it hard to read. Notice, also, spacing is not