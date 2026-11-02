When defining a function, you provide a name for the function, a variable for each argument, and a type for the result.

Put all this information together to form the first line of the function's definition:

```
double cube_volume(double side_length)
```

Next, specify the body of the function: the statements that are executed when the function is called.

The volume of a cube of side length s is s × s × s. However, for greater clarity, our parameter variable has been called side_length, not s, so we need to compute side_length * side_length * side_length.

We will store this value in a variable called volume:

```
double volume = side_length * side_length * side_length;
```

In order to return the result of the function, use the return statement:

```
return volume;
```

The body of a function is enclosed in braces. Here is the complete function:

```
double cube_volume(double side_length)
{
    double volume = side_length * side_length * side_length;
    return volume;
}
```

Let's put this function to use. We'll supply a main function that calls the cube_volume function twice.

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

When the function is called with different arguments, the function returns different results. Consider the call cube_volume(2). The argument 2 corresponds to the side_length parameter variable. Therefore, in this call, side_length is 2. The function computes side_length * side_length * side_length, or 2 * 2 * 2. When the function is called with a different argument, say 10, then the function computes 10 * 10 * 10.

Now we combine both functions into a test program. Because main calls cube_volume, the cube_volume function must be known before the main function is defined. This is easily achieved by placing cube_volume first and main last in the source file. (See Special Topic 5.1 for an alternative.)

![](bbox=[0.55, 0.85, 0.85, 0.98])

The return statement gives the function's result to the caller.

© princessdafri/Stockphoto.