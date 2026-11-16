
Note that in Listing 9.6 (betterprompt.cpp), we declared a variable named result inside the prompt function. This variable is local to the function, meaning we cannot use this particular variable outside of prompt. It also means we are free to use that same name outside of the prompt function in a different context, and that use will not interfere with the result variable within prompt. We say that result is a local variable.

We can further enhance our prompt function. Currently prompt always prints the same message. Using parameters, we can customize the message that prompt prints. Listing 9.7 (evenbetterprompt.cpp) shows how parameters are used to provide a customized message within prompt.

```
Listing 9.7: evenbetterprompt.cpp

#include <iostream>

// Definition of the prompt function
int prompt(int n)
{
    int result;
    std::cout << "Please enter integer #" << n << ": ";
    std::cin >> result;
    return result;
}

int main()
{
    int value1, value2, sum;
    std::cout << "This program adds together two integers.\n";
    value1 = prompt(1); // Call the function
    value2 = prompt(2); // Call the function again
    sum = value1 + value2;
    std::cout << value1 << " + " << value2 << " = " << sum << '\n';
}
```

In Listing 9.7 (evenbetterprompt.cpp), the parameter influences the message that it printed. The user is now prompted to enter value #1 or value #2. The call

value1 = prompt(1);

passes the value 1 to the prompt function. Since prompt's parameter is named n, the process works as if the assignment statement

n = 1;

were executed as the first action within prompt.

In the first line of the function definition:

int prompt(int n)

n is called the formal parameter. A formal parameter is used like a variable within the function's body, but it is declared in the function's parameter list; it is not declared in the function's body. A formal parameter is a parameter as used in the formal definition of the function.

At the point of the function call:

value1 = prompt(1);

the parameter (or argument) passed into the function, 1, is called the actual parameter. An actual parameter is the parameter actually used during a call of the function. When a function is called, any actual parameters are assigned to their corresponding formal parameters, and the function begins executing. Another way to say it is that during a function call, the actual parameters are bound to their corresponding formal parameters.

The parameters used within a function definition are called formal parameters. Formal parameters behave as local variables within the function's body; as such, the name of a formal parameter will not conflict with any local variable or formal parameter names from other functions. This means as a function developer you may choose a parameter name that best represents the parameter's role in the function.

![](img/e84ad11adb18201d71595b31ce6c9eff_220_0.png)

If you are writing a function, you cannot predict the caller's actual parameters. You must be able to handle any value the caller sends. The compiler will ensure that the types of the caller's parameters are compatible with the declared types of your formal parameters.

To remember the difference between formal and actual parameters, remember this:

- A formal parameter is a parameter declared and used in a function's formal definition.
- An actual parameter is a parameter supplied by the caller when the caller actually uses (invokes or calls) the function.

When the call `value1 = prompt(1);` is executed in main, and the statement `std::cout << "Please enter integer #" << n << ": ";` within the body of prompt is executed, n will have the value 1. Similarly, when the call `value2 = prompt(2);` is executed in main, and the statement `std::cout << "Please enter integer #" << n << ": ";` within the body of prompt is executed, n will have the value 2. In the case of `value1 = prompt(1);` n within prompt is bound to 1, and in the case of `value2 = prompt(2);` n within prompt is bound to 2.

A function's definition requires that all formal parameters be declared in the parentheses following the function's name. A caller does not provide actual parameter type declarations when calling the function. Given the square_root function defined in Listing 9.1 (countersquareroot.cpp), the following caller code fragment is illegal:

```
double number = 25.0;
// Legal, pass the variable's value to the function
std::cout << square_root(number) << '\n';
// Illegal, do not declare the parameter during the call
std::cout << square_root(double number) << '\n';
```

The function definition is responsible for declaring the types of its parameters, not the caller.

## 9.2 Using Functions

The general form of a function definition is

```
type name( parameterlist ) {
    body
}
```

- The type of the function indicates the type of value the function returns. Often a function will perform a calculation and the result of the calculation must be communicated back to the place where the function was invoked. The special type void indicates that the function does not return a value.
- The name of the function is an identifier (see Section 3.3). The function's name should indicate the purpose of the function.
- The parameterlist is a comma separated list of pairs of the form
    type name

where type is a C++ type and name is an identifier representing a parameter. The caller of the function communicates information into the function via parameters. The parameters specified in the parameter list of a function definition are called formal parameters. A parameter is also known as an argument. The parameter list may be empty; an empty parameter list indicates that no information may be passed into the function by the caller.
- The body is the sequence of statements, enclosed within curly braces, that define the actions that the function is to perform. The statements may include variable declarations, and any variables declared within the body are local to that function.

The body may contain only one statement, many statements, or no statements at all; regardless, the curly braces always are required.

Observe that multiple pieces of information can be passed into a function via multiple parameters, but only one piece of information can be passed out of the function via the return value. Recall the greatest

![](img/e84ad11adb18201d71595b31ce6c9eff_222_0.png)
![](img/e84ad11adb18201d71595b31ce6c9eff_222_1.png)

common divisor (also called greatest common factor) from elementary mathematics. To determine the GCD of 24 and 18 we list all of their common factors and select the largest one:

- 24: 1, 2, 3, 4, 6, 8, 12, 24
- 18: 1, 2, 3, 6, 9, 18

The greatest common divisor function is useful when reducing fractions to lowest terms; for example, consider the fraction 18/24. The greatest common divisor of 18 and 24 is 6, and so we divide the numerator and the denominator of the fraction by 6: 18/6 / 24/6 = 3/4. The GCD function has applications in other areas besides reducing fractions to lowest terms.

Consider the problem of dividing a piece of plywood 24 inches long by 18 inches wide into square pieces of maximum size without wasting any material. Since the GCD(24, 18) = 6, we can cut the plywood into twelve 6 inch x 6 inch square pieces as shown in Figure 9.2.

If we cut the plywood into squares of any other size without wasting any of the material, the squares would have to be smaller than 6 inches x 6 inches; for example, we could make forty-eight 3 inch x 3 inch squares as shown in Figure 9.3.

If we cut squares larger than 6 inches x 6 inches, not all the plywood can be used to make the squares.

## Figure 9.4 Squares too large

![](img/e84ad11adb18201d71595b31ce6c9eff_223_0.png)

Figure 9.4 shows how some larger squares would fare.

In addition to basic arithmetic and geometry, the GCD function plays a vital role in cryptography, enabling secure communication across an insecure network.

## Listing 9.8: gcdprog.cpp

```cpp
#include <iostream>

int main() {
    // Prompt user for input
    int num1, num2;
    std::cout << "Please enter two integers: ";
    std::cin >> num1 >> num2;

    // Determine the smaller of num1 and num2
    int min = (num1 < num2) ? num1 : num2;

    // 1 is definitely a common factor to all ints
    int largestFactor = 1;
    for (int i = 2; i <= min; i++)
```
