# Chapter 11: Working with Numeric Functions

# Program 11.15: Demonstrating the LAG and LAG Functions

```
data Look_Back;
input Time Temperature;
Prev_Temp = lag(Temperature);
Two_Back = lag2(Temperature);
datalines;
1 60
2 62
3 65
4 70;
```

A listing of data set Look_Back:

Figure 11.13: Listing of Data Set Look_Back

| Time | Temperature | Prev_Temp | Two_Back |
|---|---|---|--|
| 1 | 60 | - | - |
| 2 | 62 | 60 | - |
| 3 | 65 | 62 | 60 |
| 4 | 70 | 65 | 62 |

As you can see from this listing, the LAG function returns the temperature from the previous time and the LAG2 function returns the temperature from the time before that.(There is a whole family of LAG functions: Lag, LAG2, LAG3, and so on.) This program might give you the idea that the LAG function returns the value of its argument from the previous observation. This is not always true.

> Note: The correct definition of the LAG function is that it returns the value of its argument the last LAG function executed.

To help clarify this somewhat clounding definition, see if you can predict the values of X and Last_X in a program that follows:

# Program 11.16: Demonstrating What Happens When You Execute a LAG Function Conditionally

```
data Laggard;
input X @@;
if X ge 5 then Last_X = lag(X);
datalines;
9 8 7 1 2 12;
```