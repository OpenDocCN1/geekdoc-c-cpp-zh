In Listing 25, first an x variable is declared and initialized with 15. Then, the value of the x variable is left shifted two times by using the left shift operator, and the value of the x variable is displayed on the screen.

![](bbox=[0.2282, 0.2182, 0.2624, 0.2464])

> Shifting a negative number to right inserts 1 at the left for the every bit shifted to the right.

After discussing about the left and right shift operators, let’s explore the ternary operator.

# The Ternary Operator

Ternary operators are those C++ operators that work as an alternative of the if-else statement. They are called ternary operators because they work on three operands. The ternary operator is represented as ?:, which works according to the following syntax:

```
```text
result = condition ? value1 : value2
```
```

According to the preceding syntax, if the condition evaluates to true, then the value of the result will be 1 else, the result value will be 2. The preceding syntax works similar to the following if statement:

```
```cpp
if (condition)
{
    result = value1;
}
else
{
    result = value2;
}
```
```

Let’s discuss the ternary operator to understand its functionality. Listing 26 shows the use of the ternary operator (you can find the TernaryEx.cpp file on the CD in the code/chapter1 folder):

# Listing 26: Using the Ternary Operator

```
```cpp
#include <iostream.h>

int main()
{
    int x =12, y=10, result;
    result = x > y? x :y;
    cout << "Two integers are " << x << " and " << y << endl;
    cout << "The larger of the two integers is " << result << endl;
    return 0;

}
```
```