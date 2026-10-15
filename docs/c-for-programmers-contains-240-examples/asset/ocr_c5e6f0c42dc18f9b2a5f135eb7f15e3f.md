```
// Fig. 22.4: fig22_04.cpp
// Demonstrating operator keywords.
#include <iostream>
using std::boolalpha;
using std::cout;
using std::endl;

#include <iso646.h> // enables operator keywords in Microsoft Visual C++

int main()
{
    bool a = true;
    bool b = false;
    int c = 2;
    int d = 3;

    // sticky setting that causes bool values to display as true or false
    cout << boolalpha;

    cout << "a = " << a << "; b = " << b
         << "; c = " << c << "; d = " << d;

    cout << "\n\nLogical operator keywords:";
    cout << "\n  a and a: " << ( a and a );
    cout << "\n  a and b: " << ( a and b );
    cout << "\n    a or a: " << ( a or a );
    cout << "\n    a or b: " << ( a or b );
    cout << "\n    not a: " << ( not a );
    cout << "\n    not b: " << ( not b );
    cout << "\na not_eq b: " << ( a not_eq b );

    cout << "\n\nBitwise operator keywords:";
    cout << "\n c bitand d: " << ( c bitand d );
    cout << "\n c bitor d: " << ( c bitor d );
    cout << "\n    c xor d: " << ( c xor d );
    cout << "\n    compl c: " << ( compl c );
    cout << "\n c and_eq d: " << ( c and_eq d );
    cout << "\n c or_eq d: " << ( c or_eq d );
    cout << "\n c xor_eq d: " << ( c xor_eq d ) << endl;
    return 0;
} // end main
```

a = true; b = false; c = 2; d = 3

Logical operator keywords:
  a and a: true
  a and b: false
  a or a: true
  a or b: true
  not a: false
  not b: true
a not_eq b: true