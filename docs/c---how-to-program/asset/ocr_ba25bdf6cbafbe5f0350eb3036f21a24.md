```
```cpp
private:
   std::array< short, digits > integer;
}; // end class HugeInt

#endif
```
```

**Fig. 18.17** | HugeInt class definition. (Part 2 of 2.)

```
```cpp
// Fig. 18.18: HugeInt.cpp
// HugeInt member-function and friend-function definitions.
#include <cctype> // isdigit function prototype
#include "HugeInt.h" // HugeInt class definition
using namespace std;

// default constructor; conversion constructor that converts
// a long integer into a HugeInt object
HugeInt::HugeInt( long value )
{
   // initialize array to zero
   for ( short &element : integer )
      element = 0;

   // place digits of argument into array
   for ( size_t i = digits - 1; value != 0 && i >= 0; i-- )
   {
      integer[ i ] = value % 10;
      value /= 10;
   } // end for
} // end HugeInt default/conversion constructor

// conversion constructor that converts a character string
// representing a large integer into a HugeInt object
HugeInt::HugeInt( const string &number )
{
   // initialize array to zero
   for ( short &element : integer )
      element = 0;

   // place digits of argument into array
   size_t length = number.size();

   for ( size_t i = digits - length, k = 0; i < digits; ++i, ++k )
      if ( isdigit( number[ k ] ) ) // ensure that character is a digit
         integer[ i ] = number[ k ] - '0';
} // end HugeInt conversion constructor

// addition operator; HugeInt + HugeInt
HugeInt HugeInt::operator+( const HugeInt &op2 ) const
{
   HugeInt temp; // temporary result
   int carry = 0;

   for ( int i = digits - 1; i >= 0; i-- )
   {
      temp.integer[ i ] = integer[ i ] + op2.integer[ i ] + carry;
```
```

**Fig. 18.18** | HugeInt member-function and friend-function definitions. (Part 1 of 2.)