
```
std::cout << value << '\n';
```

- 8. Rewrite the following code fragment so that a multi-way if/else is used instead of the switch statement.

```cpp
int value;
char ch;
std::cin >> ch;
switch (ch) {
case 'A':
    std::cout << ch << '\n';
    value = 10;
    break;
case 'P':
case 'E':
    std::cin >> value;
    break;
case 'T':
    std::cin >> ch;
    value = ch;
case 'C':
    value = ch;
    std::cout << "value=" << value << ", ch=" << ch << '\n';
    break;
case 'W':
    value = ch + 1000;
    break;
}
std::cout << value << '\n';
```

- 9. Rewrite the following code fragment so a while loop is used instead of the for statement.

```cpp
for (int i = 100; i > 0; i--)
    std::cout << i << '\n';
```

- 10. Rewrite the following code fragment so that it uses the conditional operator instead of an if statement:

```cpp
if (value % 2 != 0)     // Is value even?
    value = value + 1;  // If not, make it even.
```

- 11. Rewrite the following code fragment so that it uses the conditional operator instead of an if/else statement:

```cpp
if (value % 2 == 0)     // Is value even?
    value = 0;          // If so, make it zero.
else
    value = value + 1;  // Otherwise, make it even.
```

- 12. Would the following multi-way if/else be a good candidate to rewrite as a switch statement? If so, rewrite the code using a switch; otherwise, explain why it is impractical to do so.

```cpp
int x, y;
std::cin >> x >> y;
if (x < 10)
    y = 10;
else if (x == 5)
    y = 5;
else if (x == y)
    y = 0;
else if (y > 10)
    x = 10;
else
    x = y;
```

## Chapter 8

## Using Functions

Suppose you must write a C++ program that computes the square root of a number supplied by the user. Listing 8.1 (computesquareroot.cpp) provides a simple implementation.

```
Listing 8.1 computesquareroot.cpp

// File squareroot.cpp

#include <iostream>

int main() {
    double input;
    // Get value from the user
    std::cout << "Enter number: ";
    std::cin >> input;
    double diff;
    // Compute a provisional square root
    double root = 1.0;

    do { // Loop until the provisional root
        // is close enough to the actual root
        root = (root + input/root) / 2.0;
        std::cout << "root is " << root << "\n";
        // How bad is the approximation?
        diff = root * root - input;
    } while (diff > 0.0001 || diff < -0.0001);

    // Report approximate square root
    std::cout << "Square root of " << input << " = " << root << "\n";
}
```

The program is based on a simple algorithm, Newton's Method, that uses successive approximations to zero in on an answer that is within 0.0001 of the true answer.

One sample run is

```
Enter number: 2
root is 1.5
root is 1.41667
root is 1.41422
Square root of 2 = 1.41422
```

The actual square root is approximately 1.4142135623730951 and so the result is within our accepted tolerance (0.0001). Another run is

```
Enter number: 100
root is 50.5
root is 26.2401
root is 15.0255
root is 10.8404
root is 10.0326
root is 10.0001
root is 10
Square root of 100 = 10
```

which is, of course, the exact answer.

While this code may be acceptable for many applications, better algorithms exist that work faster and produce more precise answers. Another problem with the code is this: What if you are working on a significant scientific or engineering application and must use different formulas in various parts of the source code, and each of these formulas involve square roots in some way? In mathematics, for example, you use square root to compute the distance between two geometric points (x1,y1) and (x2,y2) as

![](img/e84ad11adb18201d71595b31ce6c9eff_191_0.png)

and, using the quadratic formula, the solution to the equation ax^2 + bx + c = 0 is

![](img/e84ad11adb18201d71595b31ce6c9eff_191_1.png)

In electrical engineering and physics, the root mean square of a set of values {a1, a2, a3, ..., an} is

![](img/e84ad11adb18201d71595b31ce6c9eff_191_2.png)

Suppose we are writing one big program that, among many other things, needs to compute distances and solve quadratic equations. Must we copy and paste the relevant portions of the square root code in Listing 8.1 (computesquareroot.cpp) to each copy in our source code that requires a square root computation? Also, what if we develop another program that requires computing a root mean square? Will we need to copy the code from Listing 8.1 (computesquareroot.cpp) into every program that needs to compute square roots, or is there a better way to package the square root code and reuse it?

Code is made reusable by packaging it in functions. A function is a unit of reusable code. In Chapter 9 we will write our own reusable functions, but in this chapter we examine some of the functions available in the C++ standard library. C++ provides a collection of standard precompiled C and C++ code stored in libraries. Programmers can use parts of this library code within their own code to build sophisticated programs.

## Figure 8.1 Conceptual view of the square root function

![](img/e84ad11adb18201d71595b31ce6c9eff_192_0.png)

## 8.1 Introduction to Using Functions

In mathematics, a function computes a result from a given value; for example, from the function definition f(x) = 2x + 3, we can compute f(5) = 13 and f(0) = 3. A function in C++ works like a mathematical function. To introduce the function concept, we will look at the standard C++ function that implements mathematical square root.

In C++, a function is a named sequence of code that performs a specific task. A program itself consists of a collection of functions. One example of a function is the mathematical square root function. Such a function, named sqrt, is available to C and C++ programs (see Section 8.2). The square root function accepts one numeric value and produces a double value as a result; for example, the square root of 16 is 4, so when presented with 16.0, sqrt responds with 4.0. Figure 8.1 visualizes the square root function.

For the programmer using the sqrt function within a program, the function is a black box; the programmer is concerned more about what the function does, not how it does it.

This sqrt function is exactly what we need for our square root program. Listing 8.1 (computesquareroot.cpp). The new version, Listing 8.2 (standardsquareroot.cpp), uses the library function sqrt and eliminates the complex logic of the original code.

```
Listing 8.2: standardsquareroot.cpp
#include <iostream>
#include <cmath>

int main() {
    double input;

    // Get value from the user
    std::cout << "Enter number: ";
    std::cin >> input;

    // Compute the square root
    double root = sqrt(input);

    // Report result
    std::cout << "Square root of " << input << " = " << root << '\n';
}
```

The line #include <cmath> directs the preprocessor to augment our source code with the declarations of a collection of mathematical functions in the cmath library. The sqrt function is among them. Table 8.1 lists some of the other commonly used mathematical functions available in the cmath library. The compiler needs this augmented code so it can check to see if we are using the sqrt function properly.

The expression

```
sqrt(input)
```

is a function invocation, also known as a function call. A function provides a service to the code that uses it. Here, our main function is the caller that uses the service provided by the sqrt function. We say main calls, or invokes, sqrt passing it the value of input. The expression sqrt(input) evaluates to the square root of the value of the variable input. Behind the scenes—inside the black box as it were—precompiled C code uses the value of the input variable to compute its square root. There is nothing special about this precompiled C code that constitutes the sqrt function; it was written by a programmer or team of programmers working for the library vendor using the same tools we have at our disposal. In Chapter 9 we will write our own functions, but for now we will enjoy the functions that others have provided for us.

When calling a function, a pair of parentheses follow the function's name. Information that the function requires to perform its task must appear within these parentheses. In the expression

```
sqrt(input)
```

input is the information the function needs to do its work. We say input is the argument, or parameter, passed to the function. We also can say “we are passing input to the sqrt function.”

While we might say “we are passing input to the sqrt function,” the program really is not giving the function access to main's input variable. The sqrt function itself cannot change the value of main's input variable, it simply uses the variable's value to perform the computation.

The following simple analogy may help explain how the communication works between main and sqrt. The main function has work to do, but instead of doing all the work itself, it delegates some of the work (in this case the hard part) to sqrt. When main needs to compute the square root of input, it writes down the value of its input variable on a piece of paper and hands it to sqrt. main then sits idly until sqrt finishes its work. The sqrt function accepts main's note and begins working on the task (computing the square root of the number on the note main gave it). When it is finished, sqrt does two things: sqrt hands back to main a different piece of paper with the answer, and sqrt throws away the piece of paper main originally passed to it. When main receives the note from sqrt it uses the information on the note and then discards the note. The main function then can continue with its other business.

The sqrt function thus has no access to main's original input variable; it has only a copy of input, as if “written on a piece of paper.” (Similarly, if the sqrt function uses any variables to do its work, main is oblivious to them and has no way to access them.) After sqrt is finished and returns to main its computed answer, sqrt discards its copy of input (by analogy, the function “throws away” the paper with the copy of input that main gave it). Thus, during a function call the parameter is a temporary, transitory value used only to communicate information to the function. The parameter lives only as long as the function is executing.

Figure 8.2 illustrates a program's execution involving simple function calls.

Figure 8.2 shows that a program's execution begins in its main function. Here main calls the sqrt function twice. A vertical bar represents the time that a function is active, or “alive.” A function's variables
