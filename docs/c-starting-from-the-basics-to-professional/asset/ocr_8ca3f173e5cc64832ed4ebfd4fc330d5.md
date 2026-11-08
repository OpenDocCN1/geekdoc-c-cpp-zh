If the last statement in a function body executes so that the closing brace is reached, this is equivalent to executing a return statement with no expression. In a function with a return type other than void, this is an error, and the function will not compile—except for `main()`, of course.

# Function Declarations

Ex8_01.cpp works perfectly well as written, but let’s try rearranging the code so that the definition of `main()` precedes the definition of the `power()` function in the source file. The code in the program file will look like this:

```
```cpp
// Ex8_02.cpp
// Calculating powers - rearranged
import <iostream>;
import <format>;

int main()
{
    // Calculate powers of 8 from -3 to +3
    for (int i {-3}; i <= 3; ++i)
        std::cout << std::format("{:10}", power(8.0, i));

    std::cout << std::endl;
}

// Function to calculate x to the power n
double power(double x, int n)
{
    double result {1.0};
    if (n >= 0)
    {
        for (int i {1}; i <= n; ++i)
            result *= x;
    }
    else // n < 0
    {
        for (int i {1}; i <= -n; ++i)
            result /= x;
    }
    return result;
}
```
```

If you attempt to compile this, you won’t succeed. The compiler has a problem because the `power()` function that is called in `main()` is not defined yet when it is processing `main()`. The reason is that the compiler processes a source file from top to bottom. Of course, you could revert to the original version, but in some situations this won’t solve the problem. There are two important issues to consider:

+   - As you’ll see later, a program can consist of several source files. The definition of a function that is called in one source file may be contained in a separate source file.
+   - Suppose you have a function `A()` that calls a function `B()`, which in turn calls `A()`. If you put the definition of `A()` first, it won’t compile because it calls `B()`; the same problem arises if you define `B()` first because it calls `A()`.