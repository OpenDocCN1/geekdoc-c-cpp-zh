```
```cpp
// Fig. 18.11: Fig18_11.cpp
// Using an ostringstream object.
#include <iostream>
#include <string>
#include <sstream> // header for string stream processing
using namespace std;

int main()
{
   ostringstream outputString; // create ostringstream instance

   string string1( "Output of several data types " );
   string string2( "\tto an ostringstream object: " );
   string string3( "\n\t\tdouble: " );
   string string4( "\n\t\tint: " );
   string string5( "\n\t\taddress of int: " );

   double double1 = 123.4567;
   int integer = 22;

   // output strings, double and int to ostringstream outputString
   outputString << string1 << string2 << string3 << double1
      << string4 << integer << string5 << &integer;

   // call str to obtain string contents of the ostringstream
   cout << "outputString contains:\n" << outputString.str();

   // add additional characters and call str to output string
   outputString << "\nmore characters added";
   cout << "\n\nafter additional stream insertions,\n"
      << "outputString contains:\n" << outputString.str() << endl;
} // end main
```
```

```
```text
outputString contains:
Output of several data types
        double: 123.457
           int: 22
address of int: 0012F540

after additional stream insertions,
outputString contains:
Output of several data types
        double: 123.457
           int: 22
address of int: 0012F540
more characters added
```
```

**Fig. 18.11 | Using an ostringstream object.**

29 demonstrates that more data can be appended to the string in memory by simply issuing another stream insertion operation to `outputString`. Lines 30–31 display string `outputString` after appending additional characters.

An `istringstream` object inputs data from a string in memory to program variables. Data is stored in an `istringstream` object as characters. Input from the `istringstream`