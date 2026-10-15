```
// Fig. 8.4: fig08_04.cpp
// Pointer operators & and *.
#include <iostream>
using std::cout;
using std::endl;

int main()
{
    int a; // a is an integer
    int *aPtr; // aPtr is an int * -- pointer to an integer

    a = 7; // assigned 7 to a
    aPtr = &a; // assign the address of a to aPtr

    cout << "The address of a is " << &a
         << "\nThe value of aPtr is " << aPtr;
    cout << "\n\nThe value of a is " << a
         << "\nThe value of *aPtr is " << *aPtr;
    cout << "\n\nShowing that * and & are inverses of "
         << "each other.\n&aPtr = " << &aPtr
         << "\n*&aPtr = " << *&aPtr << endl;
    return 0; // indicates successful termination
} // end main
```

The address of a is 0012F580
The value of aPtr is 0012F580

The value of a is 7
The value of *aPtr is 7

Showing that * and & are inverses of each other.
&*aPtr = 0012F580
*&aPtr = 0012F580

# Fig. 8.4 | Pointer operators & and *.

Figure 8.5 lists the precedence and associativity of the operators introduced to this point. Note that the address operator (&) and the dereferencing operator (*) are unary operators on the third level of precedence in the chart.

| Operators | Associativity | Type |
|---|---|---|
| () [] | left to right | highest |
| ++ -- static_cast<type>( operand ) | left to right | unary (postfix) |
| ++ -- + - ! & * | right to left | unary (prefix) |
| * / % | left to right | multiplicative |
| + - | left to right | additive |

# Fig. 8.5 | Operator precedence and associativity. (Part 1 of 2.)