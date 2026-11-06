```
```cpp
89    else
90       for ( ; i < HugeInt::digits; i++ )
91          output << num.integer[ i ];

93    return output;
94 } // end function operator<<
```
```

**Fig. 11.24** | *HugeInt class member-function and friend-function definitions. (Part 3 of 3.)*

```
```cpp
 1    // Fig. 11.25: fig11_25.cpp
 2    // HugeInt test program.
 3    #include <iostream>
 4    #include "HugeInt.h"
 5    using namespace std;

 7    int main()
 8    {
10       HugeInt n1( 7654321 );
11       HugeInt n2( 7891234 );
12       HugeInt n3( "999999999999999999999999999999" );
13       HugeInt n4( "1" );
14       HugeInt n5;

15       cout << "n1 is " << n1 << "\nn2 is " << n2
16          << "n3 is " << n3 << "\nn4 is " << n4
17          << "\nn5 is " << n5 << "\n\n";

19       n5 = n1 + n2;
20       cout << n1 << " + " << n2 << " = " << n5 << "\n\n";

22       cout << n3 << " + " << n4 << " = " << ( n3 + n4 ) << "\n\n";

24       n5 = n1 + 9;
25       cout << n1 << " + 9 = " << n5 << "\n\n";

27       n5 = n2 + "10000";
28       cout << n2 << " + " << "10000" << " = " << n5 << endl;
29    } // end main
```
```

```
```text
n1 is 7654321
n2 is 7891234
n3 is 999999999999999999999999999999
n4 is 1
n5 is 0

7654321 + 7891234 = 15545555

999999999999999999999999999999 + 1
= 1000000000000000000000000000000

7654321 + 9 = 7654330

7891234 + 10000 = 7901234
```
```

**Fig. 11.25** | *Huge integers.*

# **11.10 (RationalNumber Class)** Create a class RationalNumber (fractions) with the following capabilities:

+   a) Create a constructor that prevents a 0 denominator in a fraction, reduces or simplifies fractions that are not in reduced form and avoids negative denominators.