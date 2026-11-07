```
```cpp
using namespace std;

void mystery1( char *, const char * ); // prototype

int main()
{
    char string1[ 80 ];
    char string2[ 80 ];

    cout << "Enter two strings: ";
    cin >> string1 >> string2;
    mystery1( string1, string2 );
    cout << string1 << endl;
} // end main

// What does this function do?
void mystery1( char *s1, const char *s2 )
{
    while ( *s1 != '\0' )
        ++s1;

    for ( ; *s1 = *s2; ++s1, ++s2 )
        ; // empty statement
} // end function mystery1
```
```

# **8.14 (What Does This Code Do?)** What does this program do?

```
```cpp
// Ex. 8.14: ex08_14.cpp
// What does this program do?
#include <iostream>
using namespace std;

int mystery2( const char * ); // prototype

int main()
{
    char string1[ 80 ];

    cout << "Enter a string: ";
    cin >> string1;
    cout << mystery2( string1 ) << endl;
} // end main

// What does this function do?
int mystery2( const char *s )
{
    int x;

    for ( x = 0; *s != '\0'; ++s )
        ++x;

    return x;
} // end function mystery2
```
```

**8.15 (Quicksort)** You’ve previously seen the sorting techniques of the bucket sort and selection sort. We now present the recursive sorting technique called Quicksort. The basic algorithm for a single-subscripted array of values is as follows: