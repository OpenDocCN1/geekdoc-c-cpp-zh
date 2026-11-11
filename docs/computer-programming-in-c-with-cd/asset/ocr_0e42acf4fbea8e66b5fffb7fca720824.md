| Operator | Meaning | Associativity |
|---|---|---|
| `<<=` | Left shift assignment | Right to left |
| `>>=` | Right shift assignment | Right to left |
| `&=` | Bitwise AND assignment | Right to left |
| `|=` | Bitwise inclusive OR assignment | Right to left |
| `^=` | Bitwise exclusive OR assignment | Right to left |
| throw | Throw an exception | None |
| `,` | Comma | Left to right |

Listing 33 shows the associativity of operators (you can find the OperatorAssEx.cpp file on the CD in the code/chapter1 folder):

# Listing 33: Showing Operator Associativity

```
```cpp
#include <iostream.h>
int main()
{
    double value;
    value = 6*2 / 6;
    cout << "The value = " << value << endl;
    return 0;
}
```
```

**Output:**

```
```text
The value =2
```
```

In Listing 33, the C++ compiler first multiplies 6 with 2 and then divides the resultant value by 6 that works from left to right.

# TEST YOUR KNOWLEDGE

Q18. Write a program to implement Operators precedence and Associativity.

Ans.

```
```cpp
#include <iostream.h>
int main()
{
    int num;
    num = 6-4*2/2;
    cout << "Final value is " << num << endl;
    return 0;
}
```
```