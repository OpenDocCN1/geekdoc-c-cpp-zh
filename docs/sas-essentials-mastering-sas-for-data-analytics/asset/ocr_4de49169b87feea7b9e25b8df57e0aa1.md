# 7.4.1 Creating and Using SAS Macro Variables

A SAS macro variable is a powerful programming concept that allows you to write code that can be easily changed to reflect new values for selected variables or code. This is accomplished with a SAS macro. A SAS variable is the symbolic name that stores information that can be used to dynamically modify SAS code through symbolic substitution.

You can think of this in a way that is similar to a "replace" in a word processor. So, SAS can dynamically (during the process of running a program) replace the value of a specified macro variable with another value you specify throughout your program code.

For example, suppose you have written a SAS program that uses the year value 2016 repeated in your code. Later on you want to update the program to use 2017 instead. If you attempt to change the entire 2016 year references in code, you might miss one. Moreover, in a program of hundreds of lines of code, this could take a long time. If you need to make many code changes as this in one long SAS program, the task becomes daunting.

A better programming technique is to use a macro variable rather than fixed code in places where you know to make changes in the future. That's one in setting where macro variables come in handy.

For example, suppose you have a program that calculates values based on a given year and a comparison based on the DEPT. you can create macro variables called YEAR and DEPT using the statements

```
%LET YEAR=2015;
LET DEPT=ENGINEERING;
```

The SAS %LET statement allows you to assign a value to a SAS macro variable. Note the % prefix to the %LET statement. Also note that these are not typical assignment statements you would like to use in a DATA step. In fact, %LET statements do not have to appear in a DAT step. This type of statement typically appears at the beginning of your program before any DATA step or PROC.

The general format for creating a macro variable is as follows:

```
%LET macrovariablename = text;
```

The value assigned to the macro variable is always a text value, even if (as in the above example) the assigned value is 2015.

Once you have created the macro variable, you refer to it in your SAS program by placing an & (ampersand) prefix to the variable name. Thus, once you define YEAR as a macro variable, you use it in a statement in the following:

```
IND_DAY=MDY(7, 4, &YEAR);
```

In this example, &YEAR is replaced by the value of the macro variable, 2015, before SAS executes the code. Thus, SAS "sees" the replaced code

```
IND_DAY=MDY(7, 4, 2015)
```

and executes that statement. In the case of the macro variable DEPT, the statement