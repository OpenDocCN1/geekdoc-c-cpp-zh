+   g. Write a C++ statement that prints the value returned by function `join` with the actual parameters "John" and "Project Manager", respectively.

+   h. Write a C++ statement that prints the next character returned by function `func3`. (Use your own actual parameters.)

10. Why do you need to include function prototypes in a program that contains user-defined functions?

11. Write the definition of a function that takes as input a `char` value and returns `true` if the character is uppercase; otherwise, it returns `false`. (4)

12. Consider the following function:

```
```cpp
int mystery(int x, double y, char ch)
{
    if (x == 0 && ch > 'A')
        return(static_cast<int>(pow(y, 2)) + static_cast<int>(ch));
    else if (x > 0)
        return(x > static_cast<int>(sqrt(y)) - static_cast<int>(ch));
    else
        return(2 * x + static_cast<int>(y) - static_cast<int>(ch));
}
```
```

What is the output of the following C++ statements? (1, 4)

+   a. `cout << mystery(0, 6.5, 'K') << endl;`
+   
+   b. `cout << mystery(4, 16.0, '#') << endl;`
+   
+   c. `cout << 2 * mystery(-11, 13.8, '8') << endl;`

13. Consider the following function: (4)

```
```cpp
int secret(int m, int n)
{
    int temp = 1;

    for (int i = 1; i < abs(n); i++)
        temp = temp * m;

    return temp;
}
```
```

+   a. What is the output of the following C++ statements?
+   
+      i. `cout << secret(2, 5) << endl;`
+   
+      ii. `cout << secret(3, -4) << endl;`
+   
+   b. What does the function secret do?

14. Write the definition of a function that takes as input the three numbers. The function returns `true` if the first number to the power of the second number equals the third number; otherwise, it returns `false`. (Assume that the three numbers are of type `double`.) (4)