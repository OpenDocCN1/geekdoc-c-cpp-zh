14. (Program) Repeat Exercise 13, but have your program declare the variable used to store the number as a double-precision variable. Run the program three times. The first time, enter an integer; the second time, enter a double-precision number; and the third time, enter a character. Using the output display, keep track of what number your program actually accepted from the data you entered. What happened, if anything, and why?

15. (For thought) a. Why do you think successful programs contain extensive data-input validity checks? (Hint: Review Exercises 13 and 14.)
b. What do you think is the difference between a data-type check and a data-reasonableness check?
c. Assume that a program requests users to enter a month, day, and year. What are some checks that could be made on the data entered?

# 3.5 Symbolic Constants

Certain constants used in a program have more general meanings that are recognized outside the program’s context. Examples of these types of constants include the number 3.1416, which is π accurate to four decimal places; 32.2 ft/sec², which is the gravitational constant; and the number 2.71828, which is Euler’s number accurate to five decimal places.

The meanings of certain other constants used in a program are defined strictly in the context of the application being programmed. For example, in a program used to determine bank interest charges, the interest rate typically appears in a number of different places throughout the program. Similarly, in a program used to calculate taxes, the tax rate might appear in many instructions. Programmers refer to these types of numbers as magic numbers. By themselves, the numbers are ordinary, but in the context of a particular application, they have a special (“magical”) meaning. When a magic number appears repeatedly in the same program, it becomes a potential source of error if the constant has to be changed. For example, if the interest rate or the sales tax rate changes, as these rates are likely to do, the programmer has the cumbersome task of changing the value everywhere it appears in the program. Multiple changes are subject to error: If just one value is overlooked and remains unchanged, when the program runs the result will be incorrect, and the source of the error will be difficult to locate.

To avoid the problem of having a magic number spread throughout a program in many places and to identify more universal constants clearly, such as π, C++ enables programmers to give these constants symbolic names. Then the symbolic name instead of the magic number can be used throughout the program. If the number ever has to be changed, the change need be made only once, at the point where the symbolic name is equated to the actual number value. To equate numbers to symbolic names, you use the const declaration qualifier, which specifies that the declared identifier is read-only after it’s initialized; it can’t be changed. Here are three examples of using this qualifier:

```
const double PI = 3.1416;
const double SALESTAX = 0.05;
const int MAXNUM = 100;
```

The first declaration statement creates a double-precision variable named PI and initializes it with the value 3.1416. The second declaration statement creates the double-precision