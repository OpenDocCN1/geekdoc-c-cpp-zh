Similarly, you could pass non-const data to a function that treats the data as if it were constant, then returns that data as a constant. In such cases, you might need to cast away the const-ness of the returned data, as we demonstrate in Fig. 22.1.

In this program, function maximum (lines 11–14) receives two C-style strings as const char * parameters and returns a const char * that points to the larger of the two strings. Function main declares the two C-style strings as non-const char arrays (lines 18–19); thus, these arrays are modifiable. In main, we wish to output the larger of the two C-style strings, then modify that C-style string by converting it to uppercase letters.

Function maximum’s two parameters are of type const char *, so the function’s return type also must be declared as const char *. If the return type is specified as only char *, the compiler issues an error message indicating that the value being returned cannot be converted from const char * to char *—a dangerous conversion, because it attempts to treat data that the function believes to be const as if it were non-const data.

```
// Fig. 22.1: fig22_01.cpp
// Demonstrating const_cast.
#include <iostream>
using std::cout;
using std::endl;

#include <cstring> // contains prototypes for functions strcmp and strlen
#include <cctype> // contains prototype for function toupper

// returns the larger of two C-style strings
const char *maximum( const char *first, const char *second )
{
    return ( strcmp( first, second ) >= 0 ? first : second );
} // end function maximum

int main()
{
    char s1[] = "hello"; // modifiable array of characters
    char s2[] = "goodbye"; // modifiable array of characters

    // const_cast required to allow the const char * returned by maximum
    // to be assigned to the char * variable maxPtr
    char *maxPtr = const_cast< char * >( maximum( s1, s2 ) );

    cout << "The larger string is: " << maxPtr << endl;

    for ( size_t i = 0; i < strlen( maxPtr ); i++ )
        maxPtr[ i ] = toupper( maxPtr[ i ] );

    cout << "The larger string capitalized is: " << maxPtr << endl;
    return 0;
} // end main
```

The larger string is: hello
The larger string capitalized is: HELLO