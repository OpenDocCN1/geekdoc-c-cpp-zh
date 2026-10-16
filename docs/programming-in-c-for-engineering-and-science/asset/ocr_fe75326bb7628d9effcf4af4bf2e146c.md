| Software Objects |  |  |  |  |
| Problem Objects | Type | Kind | Movement | Name |
| a Celsius temperature | double | varying | received (in) | tempCels |
| the equivalent Fahrenheit temperature | double | varying | returned (out) | none |

Thus, in addition to a name, most functions also have the following:

+   - **parameters**: variables declared within the function heading’s parentheses to hold the values received by the function; if no values are received, the parentheses are left empty.³
+   - a **return type**: the type of the value returned by the function or the keyword **void**, indicating the absence of type, if the function does not return a value.

A function’s specification provides this information. For our celsiusToFahrenheit() example, it tells us that

+   - it has one parameter of type double, and
+   - its return type is double.

Once we have this information, we can begin coding the function. We select a meaningful name such as tempCels for its parameter and write a **function stub**, consisting of a heading with an empty function body:

```
double celsiusToFahrenheit(double tempCels)
{
}
```

Now, all that remains is to design an algorithm that solves the problem, and then encode that algorithm within the body of this function stub.

# 6.3.1.3 A Function's Algorithm

Designing the algorithm for a function is almost the same as designing the algorithm for a program. The differences are:

+   - In a program, inputting data values needed in solving a problem is an early step in the algorithm; but in a function, the parameters already contain these values.
+   - In a program, data values computed as part of the solution are usually output; but in a function, they are returned to the calling function.

³ For example, the random-number generator function rand() from the cstdlib library has no parameters as do most functions that simply display some instructions to the user.