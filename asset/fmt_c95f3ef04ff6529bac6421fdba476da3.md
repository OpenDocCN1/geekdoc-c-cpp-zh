
`<< string1.c_str() << "\nptr1 is ";`

```
// Assign to pointer ptr1 the const char * returned by
// function data(). NOTE: this is a potentially dangerous
// assignment. If string1 is modified, pointer ptr1 can
// become invalid.
ptr1 = string1.data();

// output each character using pointer
for ( int i = 0; i < length; i++ )
    cout << *( ptr1 + i ); // use pointer arithmetic
cout << "\nptr2 is " << ptr2 << endl;
delete [] ptr2; // reclaim dynamically allocated memory
return 0;
} // end main
```

`string string1` is `STRINGS`

`string1` converted to a C-Style string is `STRINGS`

`ptr1` is `STRINGS`

`ptr2` is `STRINGS`

## Fig. 18.9 | Converting strings to C-style strings and character arrays.

modified (e.g., the string’s dynamic memory changes its address due to a member function call such as `string1.insert( 0, "abcd" );`), `ptr1` could become invalid—which could lead to unpredictable results.

Lines 32–33 use pointer arithmetic to output the character array pointed to by `ptr1`. In lines 35–36, the C-style string pointed to by `ptr2` is output and the memory allocated for `ptr2` is deleted to avoid a memory leak.

## Common Programming Error 18.4

Not terminating the character array returned by `data` with a null character can lead to execution-time errors.

## Good Programming Practice 18.1

Whenever possible, use the more robust `string` class objects rather than C-style pointer-based strings.

## 18.11 Iterators

Class `string` provides iterators for forward and backward traversal of strings. Iterators provide access to individual characters with syntax that is similar to pointer operations. Iterators are not range checked. Note that in this section we provide “mechanical examples” to demonstrate the use of iterators. We discuss more robust uses of iterators in Chapter 20. Figure 18.10 demonstrates iterators.

Lines 12–13 declare `string string1` and `string::const_iterator` `iterator1`. A `const_iterator` is an iterator that cannot modify the string—in this case the string

```cpp
// Fig. 18.10: Fig18_10.cpp
// Using an iterator to output a string.
#include <iostream>
using std::cout;
using std::endl;

#include <string>
using std::string;

int main()
{
    string string1( "Testing iterators" );
    string::const_iterator iterator1 = string1.begin();

    cout << "string1 = " << string1
         << "\n(Using iterator iterator1) string1 is: ";

    // iterate through string
    while ( iterator1 != string1.end() )
    {
        cout << *iterator1; // dereference iterator to get character
        iterator1++; // advance iterator to next character
    } // end while

    cout << endl;
    return 0;
} // end main
```

`string1 = Testing iterators`

`(Using iterator iterator1) string1 is: Testing iterators`

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_748_0.png)

through which it is iterating. Iterator `iterator1` is initialized to the beginning of `string1` with the `string` class member function `begin`. Two versions of `begin` exist—one that returns an iterator for iterating through a non-const string and a const version that returns a `const_iterator` for iterating through a const string. Line 15 outputs `string1`.

Lines 19–23 use `iterator1` to “walk through” `string1`. Class `string` member function `end` returns an iterator (or a `const_iterator`) for the position past the last element of `string1`. Each element is printed by dereferencing the iterator much as you would dereference a pointer, and the iterator is advanced one position using operator `++`.

Class `string` provides member functions `rend` and `rbegin` for accessing individual string characters in reverse from the end of a string toward the beginning. Member functions `rend` and `rbegin` return `reverse_iterators` or `const_reverse_iterators` (based on whether the string is non-const or const). We’ll use iterators and reverse iterators more in Chapter 20.

## Error-Prevention Tip 18.1

> Use `string` member function `at` (rather than iterators) when you want the benefit of range checking.

## Good Programming Practice 18.2

> When the operations involving the iterator should not modify the data being processed, use a `const_iterator`. This is another example of employing the principle of least privilege.

## 18.12 String Stream Processing

In addition to standard stream I/O and file stream I/O, C++ stream I/O includes capabilities for inputting from, and outputting to, strings in memory. These capabilities often are referred to as in-memory I/O or string stream processing.

Input from a string is supported by class `istringstream`. Output to a string is supported by class `ostringstream`. The class names `istringstream` and `ostringstream` are actually aliases defined by the typedefs

```
typedef basic_istringstream< char > istringstream;
typedef basic_ostringstream< char > ostringstream;
```

Class templates `basic_istringstream` and `basic_ostringstream` provide the same functionality as classes `istream` and `ostream` plus other member functions specific to in-memory formatting. Programs that use in-memory formatting must include the `<sstream>` and `<iostream>` header files.

One application of these techniques is data validation. A program can read an entire line at a time from the input stream into a `string`. Next, a validation routine can scrutinize the contents of the `string` and correct (or repair) the data, if necessary. Then the program can proceed to input from the `string`, knowing that the input data is in the proper format.

Outputting to a `string` is a nice way to take advantage of the powerful output formatting capabilities of C++ streams. Data can be prepared in a `string` to mimic the edited screen format. That `string` could be written to a disk file to preserve the screen image.

An `ostringstream` object uses a `string` object to store the output data. The `str` member function of class `ostringstream` returns a copy of that `string`.

Figure 18.11 demonstrates an `ostringstream` object. The program creates `ostringstream` object `outputString` (line 15) and uses the stream insertion operator to output a series of strings and numerical values to the object.

Lines 27–28 output `string string1`, `string string2`, `string string3`, `double double1`, `string string4`, `int integer`, `string string5` and the address of `int integer`—all to `outputString` in memory. Line 31 uses the stream insertion operator and the call `outputString.str()` to display a copy of the `string` created in lines 27–28. Line 34 demonstrates that more data can be appended to the `string` in memory by simply issuing another stream insertion operation to `outputString`. Lines 35–36 display `string outputString` after appending additional characters.

```cpp
// Fig. 18.11: Fig18_11.cpp
// Using a dynamically allocated ostringstream object.
#include <iostream>
using std::cout;
using std::endl;

#include <string>
using std::string;

#include <sstream> // header file for string stream processing
using std::ostringstream; // stream insertion operators

int main()
{
    ostringstream outputString; // create ostringstream instance

    string string1("Output of several data types ");
    string string2(" to an ostringstream object:");
    string string3("\n        double: ");
    string string4("\n        int: ");
    string string5("\naddress of int: ");

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
    return 0;
} // end main
```
