```
```cpp
int volume(int l, int w, int h)
{
    return l * w * h;                         //Line 10
}

void funcOne(int& x, double y, char z)
{
    x = 2 * x;                                //Line 11
    cout << "Line 12: x = " << x << ", y = "
         << y << ", z = " << z << endl;      //Line 12
}
```
```

# Sample Run:

```
```text
Line 1: a = 23, b = 48.78, ch = M
Line 2: Volume = 1
Line 3: Volume = 20
Line 4: Volume = 34
Line 5: Volume = 120
Line 12: x = 46, y = 12.34, z = B
Line 12: x = 92, y = 42.68, z = B
Line 12: x = 184, y = 34.65, z = Q
Line 9: a = 184, b = 48.78, ch = M
```
```

> > **NOTE**  In programs in this book, and as is recommended, the definition of the function `main` is placed before the definition of any user-defined functions. You must, therefore, specify the default value for a function prototype only, and the function prototype only, not in the function definition because this must occur at the first appearance of the function name.

# PROGRAMMING EXAMPLE: Classify Numbers

In this example, we use functions to rewrite the program that determines the number of odds and evens from a given list of integers. This program was first written in Chapter 5.

The main algorithm remains the same:

+   1. Initialize the variables, zeros, odds, and evens to 0.
+   2. Read a number.
+   3. If the number is even, increment the even count, and if the number is also zero, increment the zero count; otherwise, increment the odd count.
+   4. Repeat Steps 2 and 3 for each number in the list.

The main parts of the program are: initialize the variables, read and classify the numbers, and then output the results. To simplify the function main and further illustrate parameter passing, the program includes: