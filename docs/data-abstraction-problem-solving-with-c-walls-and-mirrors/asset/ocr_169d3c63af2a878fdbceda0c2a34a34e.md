the vector does not give you the entry in the removed element. You must save that entry before calling pop_back. For example, the following statements determine the current size of the vector myVector, save the value in the last element, and remove the last element from the vector:

```
int length = myVector.size(); // Find the number of elements
string last = myVector[length - 1]; // Get the string in the last element
// (subscripts start at 0)
myVector.pop_back(); // Reduce the number of elements
```

A subsequent call to myVector.size() would return length - 1, since the last element was removed.

To remove all elements from a vector and leave the empty vector, you use the method clear:
myVector.clear(); // myVector is now an empty vector

After a vector has been cleared, you must use the method push_back to add new entries.
++ Interlude 7 provides more information about vector, including these and other methods.

# A.7 Strings

Earlier, you saw that C++ provides literal character strings such as

"This is a string."

You can declare use variables that contain strings, and then manipulate the strings naturally as you manipulate integers using familiar operators. Our presentation includes only some of the possible operations on strings.

The C++ Standard Library provides the data type string. To use this library, you include the statements

```
#include <string>
using namespace std;
```

in your program.

You can declare a string variable and initialize it to the empty string by writing

string title;

You can initialize a string variable to a string literal when you declare it by writing

string title = "Walls and Mirrors"

You can subsequently assign another string to title by using an assignment statement such as

title = "Perfect's Diary";

In each of the previous examples, title has a length of 17. You can use either of the methods length or size to determine the current length of a string. title.length() and title.size() are each 17.

You can reference the individual characters in a string by using the same index notation that you use for an array. Thus, in the previous example, title[0] contains the character J and title[16] contains the character y.

You can compare strings by using the familiar comparison operators. Not only can you see whether two strings are equal, but you can also discover which two strings comes before the other.