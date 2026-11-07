```
```cpp
// Fig. 21.10: Fig21_10.cpp
// Using an iterator to output a string.
#include <iostream>
#include <string>
using namespace std;

int main()
{
   string string1( "Testing iterators" );
   string::const_iterator iterator1 = string1.begin();

   cout << "string1 = " << string1
        << "\nUsing iterator iterator1) string1 is: ";

   // iterate through string
   while ( iterator1 != string1.end() )
   {
      cout << *iterator1; // dereference iterator to get character
      ++iterator1;       // advance iterator to next character
   } // end while

   cout << endl;
} // end main
```
```

```
```text
string1 = Testing iterators
Using iterator iterator1) string1 is: Testing iterators
```
```

**Fig. 21.10**  Using an iterator to output a string.

Lines 9--10 declare string string1 and **string::const_iterator** iterator1. Recall that a const_iterator cannot be used to modify the data that you’re iterating through—in this case the string. Iterator iterator1 is initialized to the beginning of string1 with the string class member function **begin**. Two versions of begin exist—one that returns an iterator for iterating through a non-const string and a const version that returns a const_iterator for iterating through a const string. Line 12 outputs string1.

Lines 16--20 use iterator iterator1 to “walk through” string1. Class string member function **end** returns an iterator (or a const_iterator) for the position past the last element of string1. Each element is printed by dereferencing the iterator, much as you’d dereference a pointer, and the iterator is advanced one position using operator ++. In C++11, lines 10 and 16--20 can be replaced with a range-based for, as in

```
```cpp
for ( char c : string1 )
   cout << c;
```
```

Class string provides member functions **rend** and **rbegin** for accessing individual string characters in reverse from the end of a string toward the beginning. Member functions rend and rbegin return **reverse_iterators** or **const_reverse_iterators** (based on whether the string is non-const or const). Exercise 21.8 asks you to write a program that demonstrates these capabilities.

![](bbox=[0.03, 0.778, 0.087, 0.81])