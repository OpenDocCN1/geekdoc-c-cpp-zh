*The return statement gives the function's result to the caller.*

![](bbox=[0.527, 0.094, 0.839, 0.268])

Let's put this function to use. We'll supply a `main` function that calls the `cube_volume` function twice.

```
    int main()
    {
        double result1 = cube_volume(2);
        double result2 = cube_volume(10);
        cout << "A cube with side length 2 has volume " << result1 << endl;
        cout << "A cube with side length 10 has volume " << result2 << endl;

        return 0;
    }
```

When the function is called with different arguments, the function returns different results. Consider the call `cube_volume(2)`. The argument 2 corresponds to the `side_length` parameter variable. Therefore, in this call, `side_length` is 2. The function computes `side_length * side_length * side_length`, or `2 * 2 * 2`. When the function is called with a different argument, say 10, then the function computes `10 * 10 * 10`.

Now we combine both functions into a test program. Because `main` calls `cube_volume`, the `cube_volume` function must be known before the `main` function is defined. This is easily achieved by placing `cube_volume` first and `main` last in the source file. (See Special Topic 5.1 on page 203 for an alternative.)

# ### Syntax 5.1 Function Definition

```
    // Type of return value: double
    // Name of function: cube_volume
    // Type of parameter variable: double
    // Name of parameter variable: side_length
    double cube_volume(double side_length)
    {
        // Function body, executed when function is called.
        double volume = side_length * side_length * side_length;
        // return statement exits function and returns result. See page 202.
        return volume;
    }
```