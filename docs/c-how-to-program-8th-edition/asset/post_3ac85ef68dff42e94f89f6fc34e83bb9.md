
```cpp
string string1( "cat" );
string string2; // initialized to the empty string
string string3; // initialized to the empty string

string2 = string1; // assign string1 to string2
string3.assign( string1 ); // assign string1 to string3
cout << "string1: " << string1 << "\nstring2: " << string2
     << "\nstring3: " << string3 << "\n\n";

// modify string2 and string3
string2[ 0 ] = string3[ 2 ] = 'r';

cout << "After modification of string2 and string3:\n" << "string1: "
     << string1 << "\nstring2: " << string2 << "\nstring3: ";

// demonstrating member function at
for ( int i = 0; i < string3.length(); ++i )
    cout << string3.at( i );

// declare string4 and string5
string string4( string1 + "apult" ); // concatenation
string string5; // initialized to the empty string

// overloaded +=
string3 += "pet"; // create "carpet"
string1.append( "acomb" ); // create "catacomb"

// append subscript locations 4 through end of string1 to
// create string "comb" (string5 was initially empty)
string5.append( string1, 4, string1.length() - 4 );

cout << "\n\nAfter concatenation:\nstring1: " << string1
     << "\nstring2: " << string2 << "\nstring3: " << string3
     << "\nstring4: " << string4 << "\nstring5: " << string5 << endl;
} // end main
```

```text
string1: cat
string2: cat
string3: cat

After modification of string2 and string3:
string1: cat
string2: rat
string3: car

After concatenation:
string1: catacomb
string2: rat
string3: carpet
string4: catapult
string5: comb
```

**Fig. 18.1 |** Demonstrating string assignment and concatenation. *(Part 2 of 2.)*

Line 19 uses the subscript operator to assign 'r' to string3[2] (forming "car") and to assign 'r' to string2[0] (forming "rat"). The strings are then output.

Lines 25–26 output the contents of `string3` one character at a time using member function `at`. Member function `at` provides **checked access** (or range checking); i.e., going past the end of the string throws an `out_of_range` exception. The **subscript operator `[]`** does not provide checked access. This is consistent with its use on arrays.

> **Common Programming Error 18.1**
> 
> Accessing an element beyond the size of the string using the subscript operator is an un-reported logic error.

String `string4` is declared (line 29) and initialized to the result of concatenating `string1` and `"apult"` using the overloaded + operator, which for class `string` denotes concatenation. Line 33 uses the addition assignment operator, `+=`, to concatenate `string3` and `"pet"`. Line 34 uses member function `append` to concatenate `string1` and `"acomb"`.

Line 38 appends the string `"comb"` to empty string `string5`. This member function is passed the string (`string1`) to retrieve characters from, the starting subscript in the string (4) and the number of characters to append (the value returned by `string1.length() - 4`).

## 18.3 Comparing strings

Class string provides member functions for comparing strings. Figure 18.2 demonstrates class string’s comparison capabilities.

```cpp
// Fig. 18.2: Fig18_02.cpp
// Demonstrating string comparison capabilities.
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string string1( "Testing the comparison functions." );
    string string2( "Hello" );
    string string3( "stinger" );
    string string4( string2 );

    cout << "string1: " << string1 << "\nstring2: " << string2
         << "\nstring3: " << string3 << "\nstring4: " << string4 << "\n\n";

    // comparing string1 and string4
    if ( string1 == string4 )
        cout << "string1 == string4\n";
    else // string1 != string4
    {
        if ( string1 > string4 )
            cout << "string1 > string4\n";
        else // string1 < string4
            cout << "string1 < string4\n";
    } // end else
```

**Fig. 18.2** | Comparing strings. (Part 1 of 3.)

```cpp
79        else // result < 0
80            cout << "string2.compare( 0, 3, string4) < 0" << endl;
81        } // end else
82    } // end main
```

```text
string1: Testing the comparison functions.
string2: Hello
string3: stinger
string4: Hello

string1 > string4
string1.compare( string2 ) > 0
string1.compare( 2, 5, string3, 0, 5 ) == 0
string4.compare( 0, string2.length(), string2 ) == 0
string2.compare( 0, 3, string4 ) < 0
```

**Fig. 18.2** | Comparing strings. (Part 3 of 3.)

The program declares four strings (lines 9–12) and outputs each (lines 14–15). Line 18 tests string1 against string4 for equality using the overloaded equality operator. If the condition is true, "string1 == string4" is output. If the condition is false, the condition in line 22 is tested. All the string class overloaded relational and equality operator functions return bool values.

Line 29 uses string member function **compare** to compare string1 to string2. Variable result is assigned 0 if the strings are equivalent, a positive number if string1 is lexicographically greater than string2 or a negative number if string1 is lexicographically less than string2. When we say that a string is lexicographically less than another, we mean that the compare method uses the numerical values of the characters (see Appendix B, ASCII Character Set) in each string to determine that the first string is less than the second. Because a string starting with 'T' is considered lexicographically greater than a string starting with 'H', result is assigned a value greater than 0, as confirmed by the output. A lexicon is a dictionary.

Line 42 compares portions of string1 and string3 using an overloaded version of member function compare. The first two arguments (2 and 5) specify the starting subscript and length of the portion of string1 ("sting") to compare with string3. The third argument is the comparison string. The last two arguments (0 and 5) specify the starting subscript and length of the portion of the comparison string being compared (also "sting"). The value assigned to result is 0 for equality, a positive number if string1 is lexicographically greater than string3 or a negative number if string1 is lexicographically less than string3. The two pieces being compared here are identical, so result is assigned 0.

Line 55 uses another overloaded version of function compare to compare string4 and string2. The first two arguments are the same—the starting subscript and length. The last argument is the comparison string. The value returned is also the same—0 for equality, a positive number if string4 is lexicographically greater than string2 or a negative number if string4 is lexicographically less than string2. Because the two pieces of strings being compared here are identical, result is assigned 0.

Line 71 calls member function compare to compare the first 3 characters in string2 to string4. Because "Hel" is less than "Hello", a value less than zero is returned.

## 18.4 Substrings

Class string provides member function `substr` for retrieving a substring from a string. The result is a new string object that’s copied from the source string. Figure 18.3 demonstrates substr. The program declares and initializes a string at line 9. Line 13 uses member function substr to retrieve a substring from string1. The first argument specifies the beginning subscript of the desired substring; the second argument specifies the substring’s length.

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

plane

**Fig. 18.3** | Demonstrating string member function `substr`.

## 18.5 Swapping strings

Class string provides member function `swap` for swapping strings. Figure 18.4 swaps two strings. Lines 9–10 declare and initialize strings first and second. Each string is then output. Line 15 uses string member function swap to swap the values of first and second. The two strings are printed again to confirm that they were indeed swapped. The string member function swap is useful for implementing programs that sort strings.

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

**Fig. 18.4** | Using function swap to swap two strings. (Part 1 of 2.)
