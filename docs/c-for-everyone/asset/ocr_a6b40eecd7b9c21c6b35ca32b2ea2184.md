# **R5.13** Consider the following function:

```
```cpp
int f(int n)
{
    if (n <= 1) { return 1; }
    if (n % 2 == 0) // n is even
    {
        return f(n / 2);
    }
    else { return f(3 * n + 1); }
}
```
```

Perform traces of the computations f(1), f(2), f(3), f(4), f(5), f(6), f(7), f(8), f(9), and f(10).

# **R5.14** Eliminate the global variable in the code at the end of Section 5.8 by

+   a. passing the balance to the withdraw function and returning the updated balance.
+   
+   b. passing the balance as a reference parameter to the withdraw function.

# **R5.15** Given the following functions, trace the function call `print_roots(4)`.

```
```cpp
int i;

int isqrt(int n)
{
    i = 1;
    while (i * i <= n) { i++; }
    return i - 1;
}

void print_roots(int n)
{
    for (i = 0; i <= n; i++) { cout << isqrt(i) << " "; }
}
```
```

How can you fix the code so that the output is as expected (that is, 0 1 1 1 2)?

# **R5.16** Consider the following function that is intended to swap the values of two integers:

```
```cpp
void false_swap1(int& a, int& b)
{
    a = b;
    b = a;
}

int main()
{
    int x = 3;
    int y = 4;
    false_swap1(x, y);
    cout << x << " " << y << endl;
    return 0;
}
```
```

Why doesn’t the function swap the contents of x and y? How can you rewrite the function to work correctly?

# **R5.17** Consider the following function that is intended to swap the values of two integers:

```
```cpp
void false_swap2(int a, int b)
{
```
```