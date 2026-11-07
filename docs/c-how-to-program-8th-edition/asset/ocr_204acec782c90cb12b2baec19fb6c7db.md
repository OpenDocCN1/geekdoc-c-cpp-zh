# ## 18.4 Substrings

Class string provides member function `substr` for retrieving a substring from a string. The result is a new string object that’s copied from the source string. Figure 18.3 demonstrates substr. The program declares and initializes a string at line 9. Line 13 uses member function substr to retrieve a substring from string1. The first argument specifies the beginning subscript of the desired substring; the second argument specifies the substring’s length.

```
```cpp
// Fig. 18.3: Fig18_03.cpp
// Demonstrating string member function substr.
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string string1( "The airplane landed on time." );

    // retrieve substring "plane" which
    // begins at subscript 7 and consists of 5 characters
    cout << string1.substr( 7, 5 ) << endl;
} // end main
```
```

plane

**Fig. 18.3** | Demonstrating string member function `substr`.

# ## 18.5 Swapping strings

Class string provides member function `swap` for swapping strings. Figure 18.4 swaps two strings. Lines 9–10 declare and initialize strings first and second. Each string is then output. Line 15 uses string member function swap to swap the values of first and second. The two strings are printed again to confirm that they were indeed swapped. The string member function swap is useful for implementing programs that sort strings.

```
```cpp
// Fig. 18.4: Fig18_04.cpp
// Using the swap function to swap two strings.
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string first( "one" );
    string second( "two" );

    // output strings
    cout << "Before swap:\n first: " << first << "\nsecond: " << second;
```
```

**Fig. 18.4** | Using function swap to swap two strings. (Part 1 of 2.)