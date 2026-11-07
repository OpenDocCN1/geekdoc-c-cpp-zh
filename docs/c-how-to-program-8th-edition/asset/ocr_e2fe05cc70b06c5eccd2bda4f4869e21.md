```
```cpp
friend ostream &operator<<( ostream &, const PhoneNumber & );
friend istream &operator>>( istream &, PhoneNumber & );
private:
    string areaCode;  // 3-digit area code
    string exchange;  // 3-digit exchange
    string line;      // 4-digit line
}; // end class PhoneNumber

#endif
```
```

**Fig. 11.3** | PhoneNumber class with overloaded stream insertion and stream extraction operators as friend functions. (Part 2 of 2).

```
```cpp
// Fig. 11.4: PhoneNumber.cpp
// Overloaded stream insertion and stream extraction operators
// for class PhoneNumber.
#include <iostream>
#include "PhoneNumber.h"
using namespace std;

// overloaded stream insertion operator; cannot be
// a member function if we would like to invoke it with
// cout << somePhoneNumber;
ostream &operator<<( ostream &output, const PhoneNumber &number )
{
    output << "(" << number.areaCode << ") "
           << number.exchange << "-" << number.line;
    return output; // enables cout << a << b << c;
} // end function operator<<

// overloaded stream extraction operator; cannot be
// a member function if we would like to invoke it with
// cin >> somePhoneNumber;
istream &operator>>( istream &input, PhoneNumber &number )
{
    input.ignore(); // skip (
    input >> setw( 3 ) >> number.areaCode; // input area code
    input.ignore( 2 ); // skip ) and space
    input >> setw( 3 ) >> number.exchange; // input exchange
    input.ignore( 2 ); // skip dash (-)
    input >> setw( 4 ) >> number.line; // input line
    return input; // enables cin >> a >> b >> c;
} // end function operator>>
```
```

**Fig. 11.4** | Overloaded stream insertion and stream extraction operators for class PhoneNumber.

```
```cpp
// Fig. 11.5: fig11_05.cpp
// Demonstrating the PhoneNumber's overloaded stream insertion
// and stream extraction operators.
```
```

**Fig. 11.5** | Overloaded stream insertion and stream extraction operators. (Part 1 of 2.)