Array class, you’ll indeed understand the essence of object technology—crafting, using and reusing valuable classes.

The chapter concludes with discussions of how you can convert between types (including class types), problems with certain implicit conversions and how to prevent those problems.

# 10.2 Using the Overloaded Operators of Standard Library Class `string`

Figure 10.1 demonstrates many of class string’s overloaded operators and several other useful member functions, including empty, substr and at. Function empty determines whether a string is empty, function substr returns a string that represents a portion of an existing string and function at returns the character at a specific index in a string (after checking that the index is in range). Chapter 21 presents class string in detail.

```
```cpp
// Fig. 10.1: fig10_01.cpp
// Standard Library string class test program.
#include <iostream>
#include <string>
using namespace std;

int main()
{
   string s1( "happy" );
   string s2( "birthday" );
   string s3;

   // test overloaded equality and relational operators
   cout << "\n\"s1 is \"" << s1 << "\"; s2 is \"" << s2
      << "\"; s3 is \"" << s3 << "\"\n";
   cout << "\n\nThe results of comparing s2 and s1:"
      << "\nns2 == s1 yields " << ( s2 == s1 ? "true" : "false" )
      << "\nns2 != s1 yields " << ( s2 != s1 ? "true" : "false" )
      << "\nns2 > s1 yields " << ( s2 > s1 ? "true" : "false" )
      << "\nns2 < s1 yields " << ( s2 < s1 ? "true" : "false" )
      << "\nns2 >= s1 yields " << ( s2 >= s1 ? "true" : "false" )
      << "\nns2 <= s1 yields " << ( s2 <= s1 ? "true" : "false" );

   // test string member-function empty
   cout << "\nTesting s3.empty():" << endl;

   if ( s3.empty() )
   {
      cout << "s3 is empty; assigning s1 to s3;" << endl;
      s3 = s1; // assign s1 to s3
      cout << "s3 is \"" << s3 << "\"";
   } // end if

   // test overloaded string concatenation operator
   cout << "\n\ns1 = s2 yields s1 = ";
```
```

**Fig. 10.1** | Standard Library string class test program. (Part 1 of 3.)