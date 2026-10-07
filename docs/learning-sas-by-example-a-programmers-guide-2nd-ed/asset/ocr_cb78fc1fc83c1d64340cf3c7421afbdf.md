# Chapter 25: Introducing the SAS Macro Language

# 25.4 Assigning Values to Macro Variables with a %LET Statement

You can assign a value to a macro variable with a %LET statement. You usually place %LET statements in open code, that is, not inside a DATA or PROC step. Here is a simple example:

# Program 25.2: Assigning a Value to a Macro Variable with a %LET Statement

```
%let Var_List = RBC WBC Chol;
title "Using a Macro Variable List";
proc means data=Learn.Blood n mean min maxdec=1;
  var &Var_List;
run;
```

Every place in your program where you use the macro variable &Var_List, SAS substitutes the RBC WBC Chol. This is a simple but useful trick when you need to repeat lists of variables.

Here is another example of using a %LET statement. Suppose you want to generate a data set containing random integers from 1 to 100. You want the program to be flexible so that you can choose how many random numbers each time you run the program. Here is the program:

# Program 25.3: Another Example of Using a %LET Statement

```
%let n = 3;
ndata Generate;
do Subj = 1 to &n;
  x = ceil(100*rand('uniform'));
  output;
end;
run;

title "Data Set with &n Random Numbers";
proc print data=Generate noobs;
run;
```

Notice that the %let statement comes before the DATA step. When this program runs, each occurrence of &n is replaced with a 3. While it would be easy to use the SAS Program Editor to change a 3 to some other value each time you run this program, imagine that this value used many times in a longer program. By simply editing the single %LET statement, you can change the value of &n everywhere in the program.

# 25.5 Demonstrating a Simple Macro

So far, you have seen macro variables used in a program. Now it's time to see an actual SAS macro. Macros can be entire SAS programs or just pieces of SAS code. You start a macro with a %MACRO and end it with a %MEND (macro end) statement. Here is an example.