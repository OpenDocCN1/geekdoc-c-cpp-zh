
## Pitfall
ARGUMENTS IN THE WRONG ORDER

When a function is called, the computer substitutes the first argument for the first formal parameter, the second argument for the second formal parameter, and so forth. Although the computer checks the type of each argument, it does not check for reasonableness. If you confuse the order of the arguments, the program will not do what you want it to do. If there is a type violation due to an argument of the wrong type, then you will get an error message. If there is no type violation, your program will probably run normally but produce an incorrect value for the value returned by the function.

## Pitfall
USE OF THE TERMS PARAMETER AND ARGUMENT

The use of the terms formal parameter and argument that we follow in this book is consistent with common usage, but people also often use the terms parameter and argument interchangeably. When you see the terms parameter and argument, you must determine their exact meaning from context. Many people use the term parameter for both what we call formal parameters and what we call arguments. Other people use the term argument both for what we call formal parameters and what we call arguments. Do not expect consistency in how people use these two terms. (In this book we sometimes use the term parameter to mean formal parameter, but this is more of an abbreviation than a true inconsistency.)

## FUNCTIONS CALLING FUNCTIONS

A function body may contain a call to another function. The situation for these sorts of function calls is the same as if the function call had occurred in the main part of the program; the only restriction is that the function declaration (or function definition) must appear before the function is used. If you set up your programs as we have been doing, this will happen automatically, since all function declarations come before the main part of the program and all function definitions come after the main part of the program. Although you may include a function call within the definition of another function, you cannot place the definition of one function within the body of another function definition.

## Example
A ROUNDING FUNCTION

The table of predefined functions (Display 3.2) does not include any function for rounding a number. The functions ceil and floor are almost, but not quite, rounding functions. The function ceil always returns the next-highest whole number (or its argument if it happens to be a whole number). So, ceil(2.3) returns 3.0, not 2.0. The function floor always returns the nearest whole number less than (or equal to) the argument. So, floor(2.9) returns 2.0, not 3.0. Fortunately, it is easy to define a function that does true rounding. The function is defined in Display 3.6. The function round rounds its argument to the nearest integer. For example, round(2.3) returns 2, and round(2.6) returns 3.

To see that round works correctly, let's look at some examples. Consider round(2.4). The value returned is the following (converted to an int value):

```
floor(2.4 + 0.5)
```

which is floor(2.9), or 2.0. In fact, for any number that is greater than or equal to 2.0 and strictly less than 2.5, that number plus 0.5 will be less than 3.0, and so floor applied to that number plus 0.5 will return 2.0. Thus, round applied to any number that is greater than or equal to 2.0 and strictly less than 2.5 will return 2. (Since the function declaration for round specifies that the type for the value returned is int, we have type cast the computed value to the type int.)

Now consider numbers greater than or equal to 2.5; for example, 2.6. The value returned by the call round(2.6) is the following (converted to an int value):

```
floor(2.6 + 0.5)
```

which is floor(3.1), or 3.0. In fact, for any number that is greater than 2.5 and less than or equal to 3.0, that number plus 0.5 will be greater than 3.0. Thus, round called with any number that is greater than 2.5 and less than or equal to 3.0 will return 3.

Thus, round works correctly for all arguments between 2.0 and 3.0. Clearly, there is nothing special about arguments between 2.0 and 3.0. A similar argument applies to all nonnegative numbers. So, round works correctly for all nonnegative arguments.

## Display 3.6 The Function round (part 1 of 2)

Testing program for the function round

```
1 #include <iostream>
2 #include <cmath>
3 using namespace std;

4 int round(double number);
5 //Assumes number >= 0.
6 //Returns number rounded to the nearest integer.

7 int main( )
8 {
9     double doubleValue;
10    char ans;

11 do
12 {
13    cout << "Enter a double value: ";
14    cin >> doubleValue;
```

## Display 3.6 The Function round (part 2 of 2)

```
15      cout << "Rounded that number is " << round(doubleValue) << endl;
16      cout << "Again? (y/n): ";
17      cin >> ans;
18  }while (ans == 'y' || ans == 'Y');
19  cout << "End of testing.\n";
20
21  }
22
23  //Uses cmath:
24  int round(double number)
25  {
26      return static_cast<int>(floor(number + 0.5));
27  }
```

## SAMPLE DIALOGUE

Enter a double value: 9.6
Rounded, that number is 10
Again? (y/n): y
Enter a double value: 2.49
Rounded, that number is 2
Again? (y/n): n
End of testing.

## Self-Test Exercises

7. What is the output produced by the following program?

```
#include <iostream>
using namespace std;

char mystery(int firstParameter, int secondParameter);

int main()
{
    cout << mystery(10, 9) << "\n";
    return 0;
}
char mystery(int firstParameter, int secondParameter)
{
    if (firstParameter >= secondParameter)
        return 'W';
    else
        return 'H';
}
```

- 8. Write a function declaration (function prototype) and a function definition for a function that takes three arguments, all of type int, and that returns the sum of its three arguments.
- 9. Write a function declaration and a function definition for a function that takes one argument of type double. The function returns the character value ’P’ if its argument is positive and returns ’N’ if its argument is zero or negative.
- 10. Can a function definition appear inside the body of another function definition?
- 11. List the similarities and differences between how you invoke (call) a predefined (that is, library) function and a user-defined function.

## FUNCTIONS THAT RETURN A BOOLEAN VALUE

The returned type for a function can be the type bool. A call to such a function returns one of the values true or false and can be used anywhere that a Boolean expression is allowed. For example, it can be used in a Boolean expression to control an if-else statement or to control a loop statement. This can often make a program easier to read. By means of a function declaration, you can associate a complex Boolean expression with a meaningful name. For example, the statement

```
if (((rate >= 10) && (rate < 20)) || (rate == 0))
{
    ...
}
```

can be made to read

```
if (appropriate(rate))
{
    ...
}
```

provided that the following function has been defined:

```
bool appropriate(int rate)
{
    return (((rate >= 10) && (rate < 20)) || (rate == 0));
}
```

## Self-Test Exercises

- 12. Write a function definition for a function called inOrder that takes three arguments of type int. The function returns true if the three arguments are in ascending order; otherwise, it returns false. For example, inOrder(1, 2, 3) and inOrder(1, 2, 2) both return true, whereas inOrder(1, 3, 2) returns false.
- 13. Write a function definition for a function called `even` that takes one argument of type `int` and returns a `bool` value. The function returns true if its one argument is an even number; otherwise, it returns false.
- 14. Write a function definition for a function called `isDigit` that takes one argument of type `char` and returns a `bool` value. The function returns true if the argument is a decimal digit; otherwise, it returns false.

## DEFINING void FUNCTIONS

In C++ a void function is defined in a way similar to that of functions that return a value. For example, the following is a void function that outputs the result of a calculation that converts a temperature expressed in degrees Fahrenheit to a temperature expressed in degrees Celsius. The actual calculation would be done elsewhere in the program. This void function implements only the subtask for outputting the results of the calculation.

```
void showResults(double fDegrees, double cDegrees)
{
    cout.setf(ios::fixed);
    cout.setf(ios::showpoint);
    cout.precision(1);
    cout << fDegrees
         << " degrees Fahrenheit is equivalent to \n"
         << cDegrees << " degrees Celsius.\n";
}
```

As the above function definition illustrates, there are only two differences between a function definition for a void function and for a function that returns a value. One difference is that we leave the keyword void where we would normally specify the type of the value to be returned. This tells the compiler that this function will not return any value. The name void is used as a way of saying “no value is returned by this function.” The second difference is that a void function definition does not require a return statement. The function execution ends when the last statement in the function body is executed.

A void function call is an executable statement. For example, the above function `showResults` might be called as follows:

```
showResults(32.5, 0.3);
```

If the above statement were executed in a program, it would cause the following to appear on the screen:

```
32.5 degrees Fahrenheit is equivalent to
0.3 degrees Celsius.
```
