
## Programming Tip 5.1

![](img/23fb3582e93ebc95909e1de029c3d388_226_0.png)

## Function Comments

Whenever you write a function, you should *comment* its behavior. Comments are for human readers, not compilers, and there is no universal standard for the layout of a function comment. In this book, we will use the following layout:

```cpp
/**
   Computes the volume of a cube.
   @param side_length the side length of the cube
   @return the volume
*/
double cube_volume(double side_length)
{
   double volume = side_length * side_length * side_length;
   return volume;
}
```

Function comments explain the purpose of the function, the meaning of the parameter variables and return value, as well as any special requirements.

This particular documentation style is borrowed from the Java programming language. It is widely supported by C++ tools as well, for example by the Doxygen tool (www.doxygen.org).

The first line of the comment describes the purpose of the function. Each @param clause describes a parameter variable and the @return clause describes the return value.

Note that the function comment does not document the implementation (how the function does what it does) but rather the design (what the function does, its inputs, and its results). The comment allows other programmers to use the function as a "black box".

## 5.3 Parameter Passing

Parameter variables hold the argument values supplied in the function call.

In this section, we examine the mechanism of passing arguments into functions. When a function is called, its *parameter variables* are created. (Another commonly used term for a parameter variable is *formal parameter*.) In the function call, an expression is supplied for each parameter variable, called the *argument*. (Another commonly used term for this expression is *actual parameter*.) Each parameter variable is initialized with the value of the corresponding argument.

Consider the function call illustrated in Figure 3:

```cpp
double result1 = cube_volume(2);
```

![](img/23fb3582e93ebc95909e1de029c3d388_226_1.png)

A recipe for a fruit pie may say to use any kind of fruit. Here, "fruit" is an example of a parameter variable. Apples and cherries are examples of arguments.

## 5.4 Return Values

> The return statement terminates a function call and yields the function result.

You use the `return` statement to specify the result of a function. When the `return` statement is processed, the function exits *immediately*. This behavior is convenient for handling exceptional cases at the beginning:

```cpp
double cube_volume(double side_length)
{
    if (side_length < 0) { return 0; }
    double volume = side_length * side_length * side_length;
    return volume;
}
```

If the function is called with a negative value for `side_length`, then the function returns 0 and the remainder of the function is not executed. (See Figure 4.)

In the preceding example, each `return` statement returned a constant or a variable. Actually, the `return` statement can return the value of any expression. Instead of saving the return value in a variable and returning the variable, it is often possible to eliminate the variable and return a more complex expression:

```cpp
double cube_volume(double side_length)
{
    return side_length * side_length * side_length;
}
```

It is important that every branch of a function return a value. Consider the following incorrect function:

```cpp
double cube_volume(double side_length)
{
    if (side_length >= 0)
    {
        return side_length * side_length * side_length;
    } // Error
}
```

Suppose you call `cube_volume` with a negative value for the side length. Of course, you aren't supposed to call that, but it might happen as the result of a coding error. Because if the condition is not true, the `return` statement is not executed. However, the function must return *something*. Depending on the circumstances, the compiler might

![](img/23fb3582e93ebc95909e1de029c3d388_229_0.png)

**Figure 4** A return Statement Exits a Function Immediately

flag this as an error, or the function might return a random value. Protect against this problem by returning *some* safe value:

```cpp
double cube_volume(double side_length)
{
    if (side_length >= 0)
    {
        return side_length * side_length * side_length;
    }
    return 0;
}
```

The last statement of every function ought to be a return statement. This ensures that *some* value gets returned when the function reaches the end.

### Common Error 5.1: Missing Return Value

![](img/23fb3582e93ebc95909e1de029c3d388_230_0.png)

A function always needs to return something. If the code of the function contains several branches, make sure that each one of them returns a value:

```cpp
int sign(double x)
{
    if (x < 0) { return -1; }
    if (x > 0) { return 1; }
    // Error: missing return value if x equals 0
}
```

This function computes the sign of a number: -1 for negative numbers and +1 for positive numbers. If the argument is zero, however, no value is returned. Most compilers will issue a warning in this situation, but if you ignore the warning and the function is ever called with an argument of 0, a *random quantity* will be returned.

### Special Topic 5.1: Function Declarations

![](img/23fb3582e93ebc95909e1de029c3d388_230_1.png)

It is a compile-time error to call a function that the compiler does not know, just as it is an error to use an undefined variable. You can avoid this error if you define all functions before they are first used. First define lower-level helper functions, then the mid-level workhorse functions, and finally `main` in your program.

Some programmers prefer to list the `main` function first in their programs. If you share that preference, you need to learn how to declare the other functions at the top of the program. A declaration of a function lists the return type, function name, and parameter variables, but it contains no body:

```cpp
double cube_volume(double side_length);
```

This is an advertisement that promises that the function is implemented elsewhere. It is easy to distinguish declarations from definitions: Declarations end in a semicolon, whereas definitions are followed by a `{ ... }` block. Declarations are also called *prototypes*.

In a function prototype, the names of the parameters are optional. You could also write

```cpp
double cube_volume(double);
```

However, it is a good idea to include parameter names in order to document the purpose of each parameter.

The declarations of common functions such as `pow` are contained in header files. If you have a look inside `<cmath>`, you will find the declaration of `pow` and the other math functions.

Here is an alternate organization of the cube.cpp file:

```cpp
#include <iostream>

using namespace std;

// Declaration of cube_volume
double cube_volume(double side_length);

int main()
{
    double result1 = cube_volume(2);  // Use of cube_volume
    double result2 = cube_volume(10);
    cout << "A cube with side length 2 has volume " << result1 << endl;
    cout << "A cube with side length 10 has volume " << result2 << endl;
    return 0;
}

// Definition of cube_volume
double cube_volume(double side_length)
{
    return side_length * side_length * side_length;
}
```

If you prefer this approach, go ahead and use it in your programs. You just need to be aware of one drawback. Whenever you change the name of a function or one of the parameter types, you need to fix it in both places: in the declaration and in the definition.

### How To 5.1 — Implementing a Function

![](img/23fb3582e93ebc95909e1de029c3d388_231_0.png)

A function is a computation that can be used multiple times with different parameters, either in the same program or in different programs. Whenever a computation is needed more than once, turn it into a function.

To illustrate this process, suppose that you are helping archaeologists who research Egyptian pyramids. You have taken on the task of writing a function that determines the volume of a pyramid, given its height and base length.

- **Step 1** Describe what the function should do.

  Provide a simple English description, such as “Compute the volume of a pyramid whose base is a square.”

- **Step 2** Determine the function’s “inputs”.

  Make a list of *all* the parameters that can vary. It is common for beginners to implement functions that are overly specific. For example, you may know that the great pyramid of Giza, the largest of the Egyptian pyramids, has a height of 146 meters and a base length of 230 meters. You should *not* use these numbers in your calculation, even if the original problem only asked about the great pyramid. It is just as easy—and far more useful—to write a function that computes the volume of *any* pyramid.

![](img/23fb3582e93ebc95909e1de029c3d388_231_1.png)
