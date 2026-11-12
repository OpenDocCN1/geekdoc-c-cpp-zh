
Standard Template Library, or STL. The STL is a collection of data types you can use in your programs. These data types are not part of the official C++ language, but they have been added to the built-in data types. Section A.9 discusses libraries such as the STL and their usefulness.

To use a vector in your program, you must begin it with the following statements:

```cpp
#include <vector>
using namespace std;
```

You can declare a vector in one of three ways:

- If you know how many elements you want in the vector, you can place the type of data it will hold in angle brackets and the number of elements in parentheses:

```cpp
vector<double> firstVector(10); // Vector to hold 10 doubles
vector<string> myVector(12); // Vector to hold 12 strings
```

The size you specify when declaring the vector is only its initial size. As you will see, a vector can grow in size when you add entries.

- You can place initial values into a vector when you declare it, by writing a second argument:

```cpp
vector<int> intVector(5, -1); // Vector to hold 5 integers, initialized to -1
```

When the elements in the vector are allocated, they are given the value of the second argument.

- You can also create an empty vector—a vector with no elements—by omitting its size and the parentheses:

```cpp
vector<char> letterVector; // An empty vector of characters
```

### Access vector entries using [] just as you would an array

You can store or access items in a vector by using the [] operator, just as you would when using an array. As for an array, the subscripts that identify elements in a vector start at 0 and go to s - 1, where s is the current size of the vector. The following statements are examples of accessing an existing value in a vector and changing the value of an existing entry:

```cpp
double x = firstVector[5]; // Places sixth entry in x
myVector[3] = "This is a sample string."; // Sets fourth entry's value
```

### size returns the number of elements in the vector

By calling the size method, you can determine whether the vector is full. This is an important advantage that a vector has over an array.

If the vector is either full or has no elements—that is, if it was created without elements, as letterVector was previously—you can still add new values by using the method push_back. The push_back method accepts an argument and adds it after the last element of the vector. In other words, it pushes the value onto the back of the vector.

### push_back places its argument into a new element at the back of a vector

Earlier, we declared a ten-element vector firstVector that could hold data of type double. If that vector was full, and we needed to add the additional values 2.3 and 3.4, we could use the push_back method:

```cpp
firstVector.push_back(2.3); // Grow vector and store value
firstVector.push_back(3.4); // Grow vector and store value
```

At this point, calling the size method would return 12, since two additional elements have been added to the vector.

### pop_back removes the last element from a vector

You also can reduce the size of a vector by removing either its last element or all of its elements. To remove only the last element, you can use the pop_back method. This method shortens the vector but does not give you the entry in the removed element. You must save that entry before calling pop_back. For example, the following statements determine the current size of the vector myVector, save the value in the last element, and then remove the last element from the vector:

```cpp
int length = myVector.size(); // Find the current number of elements
string last = myVector[length - 1]; // Get the string in the last element
myVector.pop_back(); // subscripts start at 0
// Reduce the number of elements
```

A subsequent call to myVector.size() would return length - 1, since the last element was removed.

To remove all elements from a vector and leave the vector empty, you use the method clear:

```cpp
myVector.clear(); // myVector is now an empty vector
```

After a vector has been cleared, you must use the method push_back to add new entries.

C++ Interlude 7 provides more information about vector, including these and other methods.

### clear removes all elements from a vector so it has a size of 0

## A.7 Strings

Earlier, you saw that C++ provides literal character strings such as

> "This is a string."

You can declare and use variables that contain such strings, and then manipulate the strings as naturally as you manipulate integers by using familiar operators. Our presentation includes only some of the possible operations on strings.

The C++ Standard Library provides the data type string. To use this library, you include the statements

```cpp
#include <string>
using namespace std;
```

in your program.

You can declare a string variable title and initialize it to the empty string by writing

```cpp
string title;
```

You can initialize a string variable to a string literal when you declare it by writing

```cpp
string title = "Walls and Mirrors";
```

You can subsequently assign another string to title by using an assignment statement such as

```cpp
title = "J Perfect's Day";
```

In each of the previous examples, title has a length of 17. You use either of the methods length or size to determine the current length of a string. Thus, title.length() and title.size() are each 17.

You can reference the individual characters in a string by using the same index notation that you use for an array. Thus, in the previous example, title[0] contains the character J and title[16] contains the character y.

You can compare strings by using the familiar comparison operators. Not only can you see whether two strings are equal, but you can also discover which of two strings comes before the other.

The ordering of two strings is analogous to alphabetic ordering, but you use the ASCII table instead of the alphabet. Thus, the following relationships are all true:

- "dig" < "dog"
- "Star" < "star" (because 'S' < 's')
- "start" > "star"
- "d" > "abc"

You can concatenate two strings to form another string by using the + operator. That is, you place one string after another to form another string. For example, if

```cpp
string str1 = "Com";
```

the statements

```cpp
string str2 = str1 + "puter";
str1 += "puter";
```

assign the string "Computer" to each of str2 and str1. Similarly, you can append a single character to a string, as in

```cpp
str1 += 's';
```

You can manipulate a portion of a string by using the method `substr(position, length)`.

```cpp
substr(position, length)
```

The first argument specifies the position of the beginning of the substring (remember that 0 is the position of the first character in the string). The second argument is the length of the substring. For example,

```cpp
title.substr(2, 7)
```

is the string "Perfect".

To perform input and output with C++ strings, you must include the library iostream by writing the statement

```cpp
#include <iostream>
```

in your program. For example, you then can display the contents of a string variable by executing

```cpp
title = "Walls and Mirrors";
cout << title << "\n";
```

The result is Walls and Mirrors. The operator << writes the entire string, including the blanks

You can read a string of characters into a string variable. For example, when the statement

```cpp
cin >> title;
```

reads the data line

```
Jamie Perfect's Diary
```

it assigns the string "Jamie" to title. Whitespace in the input line terminates the read operation for a string. To read the entire line of input, including its blank characters, you write

```cpp
getline(cin, title);
```
