# Chapter 8 Adventures in Functions

+   6. The following are some desired effects. Indicate whether each can be accomplished with default arguments, function overloading, both, or neither. Provide appropriate prototypes.

+   a mass (density, volume) returns the mass of an object having a density of density and a volume of volume, whereas mass (density) returns the density of density and a volume of 1.0 cubic meters. All quantities are type double.

+   b repeat (10, "I'm OK") displays the indicated string 10 times, and repeat("But you're kind of stupid") displays the indicated string 5 times.

+   c average (3,6) returns the int average of two arguments, and average (3.0, 6.0) returns the double average of two double average.

+   d mangle("I'm glad to meet you") returns the character I or a pointer to the string "I'm mad to gleet you", depending on whether you assign the return value to a char variable or a char* variable.

+   7. Write a function that returns the larger of its arguments.

+   8. Given the template of Chapter Review Question 7 and the box structure of Chapter Review Question 4, provide a template specialization that takes two box arguments and returns the one with the larger volume.

+   9. What types are assigned to v1, v2, v3, v4, and v5 in the following code (assuming the code is part of a complete program)?

```
int g(int x);
...
float m = 5.5f;
float &rm = m;
decltype(m) v1 = m;
decltype(rm) v2 = m;
decltype ((m)) v3 = m;
decltype(g(100)) v4;
decltype(2.0 * m) v5;
```

# Programming Exercises

+   1. Write a function that normally takes one argument, the address of a string, and prints that string once. However, if a second, type int, argument is provided and is nonzero, the function should print the string a number of times equal to the number of times function has been called at that point. (Note that the number of times the string is printed is not equal to the value of the second argument; it is