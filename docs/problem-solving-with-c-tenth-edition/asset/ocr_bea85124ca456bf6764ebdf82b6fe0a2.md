Although unnamed numeric constants are allowed in a program, you should seldom use them. It often makes sense to use unnamed number constants for well-known, easily recognizable, and unchangeable quantities, such as 100 for the number of centimeters in a meter. However, all other numeric constants should be given names in the fashion we just described. This will make your programs easier to read and easier to change.

Display 2.17 contains a simple program that illustrates the use of the declaration modifier const.

# Naming Constants with the const Modifier

When you initialize a variable inside a declaration, you can mark the variable so that the program is not allowed to change its value. To do this, place the word const in front of the declaration, as described below:

# SYNTAX

```
const Type_Name variableName = Constant;
```

# EXAMPLES

```
const int MAX_TRIES = 3;
const double PI = 3.14159;
```

# SELF-TEST EXERCISES

35. The following if-else statement will compile and run without any problems. However, it is not laid out in a way that is consistent with the other if-else statements we have used in our programs. Rewrite it so that the layout (indenting and line breaks) matches the style we used in this chapter.

```
if (x < 0) {x = 7; cout << "x is now positive.";}
else {x = - 7; cout << "x is now negative.";}
```

36. What output would be produced by the following two lines (when embedded in a complete and correct program)?

```
//cout << "Hello from";
cout << "Self-Test Exercise";
```

37. Write a complete C++ program that asks the user for a number of gallons and then outputs the equivalent number of liters. There are 3.78533 liters in a gallon. Use a declared constant. Since this is just an exercise, you need not have any comments in your program.