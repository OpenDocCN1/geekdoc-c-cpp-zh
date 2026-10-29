
## ASSIGNMENT/MODIFIERS

| string_Object1 = string_Object2; | Allocates space and initializes it to string_Object2's data, releases memory allocated for string_Object1, sets string_Object1's size to that of string_Object2. |
| string_Object1 += string_Object2; | Character data of string_Object2 is concatenated to the end of string_Object1; the size is set appropriately. |
| string_Object.empty( ) | Returns true if string_Object is an empty string; otherwise, returns false. |
| string_Object1 + string_Object2 | Returns a string that has string_Object2's data concatenated onto the end of string_Object1's data. The size is set appropriately. |
| string_Object1.insert(Position, string_Object2); | Inserts string_Object2 into string_Object1 beginning at Position. |
| string_Object.remove(Position, Length); | Removes substring of size Length starting at Position. |

## COMPARISONS

| string_Object1 == string_Object2<br>string_Object1 != string_Object2 | Compare for equality or inequality; returns a Boolean value. |
| string_Object1 < string_Object2<br>string_Object1 > string_Object2<br>string_Object1 <= string_Object2<br>string_Object1 >= string_Object2 | Lexicographical comparisons. |

## FINDS

| string_Object1.find(string_Object2) | Returns index of the first occurrence of string_Object2 in string_Object1. |
| string_Object1.find(string_Object2, Position) | Returns index of the first occurrence of string_Object2 in string_Object1; the search starts at Position. |
| string_Object1.find_first(string_Object2, Position) | Returns the index of the first instance in string_Object1 of any character in string_Object2, starting the search at Position. |
| string_Object1.find_first_not_of(string_Object2, Position) | Returns the index of the first instance in string_Object1 of any character not in string_Object2, starting the search at Position. |

## Random Number Generator

| FUNCTION DECLARATION | DESCRIPTION | HEADER FILE |
|---|---|---|
| int random(int); | The call random(n) returns a pseudorandom integer greater than or equal to 0 and less than or equal to n − 1. (Not available in all implementations. If not available, then you must use rand.) | cstdlib |
| int rand(); | The call rand() returns a pseudorandom integer greater than or equal to 0 and less than or equal to RAND_MAX. RAND_MAX is a predefined integer constant that is defined in cstdlib. The value of RAND_MAX is implementation dependent but will be at least 32767. | cstdlib |
| void srand(unsigned int); | Reinitializes the random number generator. The argument is the seed. Calling srand multiple times with the same argument will cause rand or random (whichever you use) to produce the same sequence of pseudorandom numbers. If rand or random is called without any previous call to srand, the sequence of numbers produced is the same as if there had been a call to srand with an argument of 1. | cstdlib |

## Trigonometric Functions

These functions use radians, not degrees.

| FUNCTION DECLARATION | DESCRIPTION | HEADER FILE |
|---|---|---|
| double acos(double); | Arc cosine | cmath |
| double asin(double); | Arc sine | cmath |
| double atan(double); | Arc tangent | cmath |
| double cos(double); | Cosine | cmath |
| double cosh(double); | Hyperbolic cosine | cmath |
| double sin(double); | Sine | cmath |
| double sinh(double); | Hyperbolic sine | cmath |
| double tan(double); | Tangent | cmath |
| double tanh(double); | Hyperbolic tangent | cmath |

This page intentionally left blank

## Old and New Header Files

In this book, we have used the header files for standard libraries that are part of the most recent ANSI/ISO C++ standard. If you have an older compiler, you may need to use the older header files. In the following, we list the new header file names that we have used in this book along with their corresponding older header file names. If the new header files do not work for you, then try the older header file names instead.

If your compiler requires the older header file names, then it also may not accommodate namespaces. In that case, you may have to eliminate all references to namespaces. If you have a compiler that requires the older header file names and/or does not support namespaces, you should consider obtaining a new compiler that comes closer to meeting the new standard.

| NEW HEADER FILE | CORRESPONDING OLDER HEADER FILE |
|---|---|
| cassert | assert.h |
| cctype | ctype.h |
| cstddef | stddef.h |
| cstdlib | stdlib.h |
| cmath | math.h |
| cstring | string.h |
| fstream | fstream.h |
| iomanip | iomanip.h |
| iostream | iostream.h |
| string | string or no corresponding library |

This page intentionally left blank

This appendix briefly covers selected language features that were introduced in C++11. For a more complete reference, consult a more advanced textbook or the ISO C++ Standard online at https://isocpp.org/.

## std::array

The standard container array is included in the <array> library and allows you to use a vector-like notation for random access into a fixed-size sequence of elements. Essentially, the container allows you to safely access array elements like a vector but with the performance and minimal storage requirements of a regular array.

The following example shows how to create an array of six integers while initializing the first three elements. The remaining three elements are automatically initialized to 0, so we don’t have the problem of unknown uninitialized values as we do with standard arrays.

```
#include <iostream>
#include <array>
using namespace std;

...
```

```
array<int,6> a = {5, 2, 4};
cout << "Size of array: " << a.size() << endl;
cout << "Element 0: " << a[0] << endl;
cout << "Setting index 4 to 100." << endl;
a[4] = 100;
cout << "Array contains: " << endl;
for (int element : a)
    cout << element << endl;
```

## Sample Dialogue

```
Size of array: 6
Element 0: 5
Setting index 4 to 100.
Array contains:
5
2
4
0
100
0
```

Just like a vector but unlike a standard array, we can retrieve the size of the array using the size() function. We can also read and set the contents of the array using the traditional [] notation. Attempts to read a value out of range returns 0, and attempts to set a value out of range has no effect. Note that indices 3 and 5 in the array get set to the default value of 0.

We can use the same functions that are available to vectors. For example, if we include <algorithm>, then we can sort the array within the ranges specified by the iterators begin() and end():

```
std::sort(a.begin(), a.end());
cout << "After sort, array contains: " << endl;
for (int element : a)
    cout << element << endl;
```

The output is the array in sorted order:

```
After sort, array contains:
0
0
2
4
5
100
```

## Regular Expressions

A full treatise on regular expressions is beyond the scope of this book, but a summary of regular expressions and some examples in C++ are described here. At the time of this writing many compilers do not support the C++11 regular expression library, so check your compiler to see if the <regex> library is supported. For those familiar with regular expressions, the new C++11 standard supports the Javascript and POSIX formats.

Formally, a regular expression provides a way to describe a language from the class of regular languages. For our purposes we’ll think of a regular expression as a way to describe a pattern that can be used to match a sequence of text. For example, we could use a regular expression to see whether a string of text contains a date in the MM-DD-YYYY format. Without regular expressions we would have to write code ourselves to process the text, which could be difficult for complicated patterns.

Here are the basic regular expressions:

| REGULAR EXPRESSION | MEANING |
|---|---|
| Letter or digit | The same letter or digit. For example, the regular expression a matches the text a, and the regular expression abc123 matches the text abc123. |
| . | Matches any single character |
| \| | Union or logical OR |
| R? | The regular expression R appears 0 or 1 time. |
| R+ | The regular expression R repeats consecutively 1 or more times. |
| R* | The regular expression R repeats consecutively 0 or more times. |
| R{n} | The regular expression R repeats consecutively n times. |
| R{n,m} | The regular expression R repeats consecutively n to m times. |
| ^ | Beginning of the text |
| $ | End of the text |
| [list of elements] | Match any of the elements. For example, [abcd] matches a, b, c, or d. |
| [element1-elementN] | Match any of the elements in the range. For example, [a-zA-Z] matches any uppercase or lowercase letter. |
| ( ) | Precedence and expression grouping |

Here are examples of some simple regular expressions:

| DESCRIPTION | REGULAR EXPRESSION |
|---|---|
| Three a's followed by three b's | aaa bbb or a{3}b{3} |
| Any sequence of zero or more a's | a* |
| One or more a's followed by any sequence of b's | a+b* |
| The rules for an identifier—that is, a letter or underscore followed by any sequence of letters, digits, or underscores | [a-zA-Z_] [a-zA-Z0-9_]* |

The C++11 regular expression library includes many useful character classes. Some of them are listed in the following table:

| REGULAR EXPRESSION | MEANING |
|---|---|
| \d | A single digit |
| \D | A non-digit |
| \s | A whitespace character (e.g., tab, newline, space) |
| \w | A word character |
