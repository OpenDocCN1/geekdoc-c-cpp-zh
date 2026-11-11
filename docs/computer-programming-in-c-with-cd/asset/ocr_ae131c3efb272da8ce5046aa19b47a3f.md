**Table 8: Arithmetic Assignment Operators**

| Operator | Meaning | Associativity |
|---|---|---|
| %= | Modulus assignment | Right to left |
| &= | Bitwise AND assignment | Right to left |
| *= | Multiplication assignment | Right to left |
| /= | Division assignment | Right to left |
| ^= | Bitwise XOR assignment | Right to left |
| |= | Bitwise OR assignment | Right to left |
| += | Addition assignment | Right to left |
| -= | Subtraction assignment | Right to left |
| <= | Less than equal to assignment | Left to right |
| >= | Greater than equal to assignment | Left to right |
| <<= | Left shift assignment | Right to left |
| >>= | Right shift assignment | Right to left |

Listing 17 shows the use of arithmetic assignment operators (you can find the ArithAssEx.cpp file on the CD in the code/chapter1 folder):

# Listing 17: Using Arithmetic Assignment Operators

```
```cpp
#include <iostream.h>

int main()
{
    int x=10, y=8, z=9;
    x *=2;
    y +=2;
    z -=2;
    cout << "x * 2 = " << x << endl;
    cout << "y + 2 = " << y << endl;
    cout << "z - 2 = " << z << endl;
    return 0;
}
```

**Output:**

```text
x * 2 = 20
y + 2 = 10
z - 2 = 7
```
```