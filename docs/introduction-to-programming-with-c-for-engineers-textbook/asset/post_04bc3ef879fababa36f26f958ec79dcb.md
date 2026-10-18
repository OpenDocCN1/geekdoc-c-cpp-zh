
## 3.1 Constants and Variables – Built-In Data Types, Their Range, and Initialization

Other parameters of basic types, such as values of lowest, min, max, etc. can be determined using the numeric_limits< T > class (from the limits), as shown in Listing 3.1.

Listing 3.1 Displaying values and measuring the size in bytes of basic C++ built-in data types (from CppBookCode, Variables.cpp).

```cpp
#include <limits>    // for basic types' limits
using std::cout, std::endl, std::numeric_limits;

    // Print basic facts about char
cout << "bytes of char = " << sizeof( char )    << endl;
cout << "char lowest = "    << +numeric_limits< char >::lowest()    << endl;
cout << "char min = "    << +numeric_limits< char >::min()    << endl;
cout << "char max = "    << +numeric_limits< char >::max()    << endl;

    // Print basic facts about int
cout << "bytes of int = "    << sizeof( int )    << endl;
cout << "int lowest = "    << numeric_limits< int >::lowest()    << endl;
cout << "int min = "    << numeric_limits< int >::min()    << endl;
cout << "int max = "    << numeric_limits< int >::max()    << endl;
```

To use numeric_limits, we need to include the limits header, as shown on line [1]. On lines [7-9], we print the lowest, min, and max value of the type char. However, to properly display values, we use a small trick here: adding a + sign in front of the numeric_limits objects. This causes the values to be treated as integers and displayed properly.

To store a value, we need to check whether the chosen representation has a sufficient number of bits. In the following example, we simply ask if type long is sufficient to store the number containing up to 11 digits. The computations are simple, but they require calling the log function to return a value of the natural logarithm, as shown on line [18] of Listing 3.2. The answer to the question of whether long is long enough is found using the comparison (<) on lines [18-19]. This true or false result goes to the bool variable longFitFlag.

```cpp
    // Check whether long is long enough to store 11-digit values
const int bits_in_byte = 8;
bool longFitFlag = ( std::log( 9999999999.0 ) / std::log( 2.0 ) + 1 ) < sizeof( long ) * bits_in_byte - 1;
```

On line [21], a message is displayed depending on the value of the flag longFitFlag. To check it, the conditional ? : operator used, the details of which are presented in GROUP 15 (Table 3.15). Finally, the following is shown in the terminal window:

bytes of char = 1
char lowest = -128
char min = -128
char max = 127
bytes of int = 4
int lowest = -2147483648
int min = -2147483648
int max = 2147483647
We cannot store 11 digits in long in this system

We see that in this system, long is not long enough to store a value composed of 11 digits. Also, we need to be very careful here, since long denotes a signed type. That is, it can store both positive and negative values. This means one bit needs to be used for sign representation. Hence, 1 is subtracted on line [19]. Further differences between signed and unsigned types are discussed in Section 7.1.4. As a rule of thumb, if no specific requirements are set, signed integers should be chosen, and types should not be mixed.

`wchar_t` can be used to store all kinds of international characters. The following code snippet shows how to create and initialize a wide character, as well as how to assign text composed of wide characters using the `std::wstring` object.

```cpp
wchar_t pl_letter = L'A';
wcout << pl_letter << L" needs " << sizeof( pl_letter ) << L" bytes." << endl;

std::wstring holiday_pl( L"święto" );

// We cannot use sizeof here - we need to call size()
size_t holiday_pl_len = holiday_pl.size();

std::wcout << holiday_pl << L" has " << holiday_pl_len << L" letters\n";
```

Also note that to display wide characters properly, we need to use `std::wcout` rather than `std::cout`. In addition, on some platforms, we need to call a platform-specific function to display the national letters properly. The results of running the previous code are as follows:

```
A needs 2 bytes.
święto has 6 letters
```

Finally, note that the wide text literals begin with the prefix L. To conclude, if we write applications that can be used in international markets, using `wchar_t`, `wstring`, `wcout`, etc. from the start is a good option. We will see examples in later chapters of this book.

## Things to Remember

+   - Choose meaningful and readable names (identifiers) for objects (variables, constants, functions, classes, etc.)
+   - Choose the proper data type for computations
+   - Prefer signed types
+   - Always initialize variables. For zero-initialization, it is sufficient to add `{ }`

## 3.2 Example Project – Collecting Student Grades

So far, we have seen how to define and use single variables and constants of different types. However, quite frequently, we need to store many such objects one after the other. Sometimes we do not know how many will be needed. To do this, we can use a data structure called a *vector* (or an *array*).³ A vector containing four numerical objects is depicted in Figure 3.2.

**Figure 3.2** A vector is composed of a number of objects occupying contiguous space in memory. Here we have *N* = 4 objects that can store floating-point data. Each cell of a vector can be accessed by providing its index. The first element is at index 0, and the last is at index *N* − 1.

To begin with, a vector is a data structure with the following characteristics:

+   - It contains objects of the same type
+   - The objects are densely placed in memory, i.e. one after another (no holes)
+   - Each object in a vector can be accessed by providing its *index* to the *subscript operator* `[ ]`. The valid indices are 0 to *N* − 1, where *N* denotes the number of elements in the vector

In C++, there are many ways of creating vectors. The most flexible is to use the `std::vector` object from the SL library, which

+   - Can be empty at the start
+   - Can be attached to new objects once they become available
+   - Contains many useful functions

Before we go into detail about what `std::vector` can do for us, let’s start with a simple example program in Listing 3.3. Its purpose is to collect students’ grades and compute their rounded average.

> ³ The term *array* is usually reserved for fixed-sized structures (Section 3.10); *vector* is used for objects with dynamically changing size.

Listing 3.3 A program to collect and compute average student grades (in *StudentGrades, main.cpp*).

```cpp
#include <vector>       // A header to use std::vector
#include <iostream>     // Headers for input and output
#include <iomanip>      // and output formatting
#include <cmath>         // For math functions

// Introduce these, to write vector instead of std::vector
using std::cout, std::cin, std::endl, std::vector;

int main()
{
    cout << "Enter your grades" << endl;

    vector< double >   studentGradeVec; // An empty vector of doubles

    // Collect students' grades
    for( ; ; )
    {
        double grade {};

        cin >> grade;

        // If ok, push new grade at the end of the vector
        if( grade >= 2.0 && grade <= 5.0 )
            studentGradeVec.push_back( grade );

        cout << "Enter more? [y/n] ";
        char ans {};
        cin >> ans;

        if( ans == 'n' || ans == 'N' )
            break; // The way to exit the loop
    }
}
```

To use `std::vector` and to be able to read and write values, a number of standard headers need to be included, as on lines [1–3]. Then, to avoid repeating the `std::` prefix over and over again, on line [7], common names from the `std` namespace are introduced into our scope with the help of the `using` directive. We already know the role of the `main` function, which starts on line [10]: it defines our C++ executable. Then, the central part is the definition of the vector object on line [15]. Notice that the type of objects to store needs to be given in `< >` brackets. To be able to store objects, the vector class is written in a generic fashion with the help of the template mechanism, which will be discussed in Section 4.7.

Then, on line [18], the `for` loop starts (see Section 3.13.2.2). Its role is to collect all grades entered by the user. However, we do not know how many will be entered. Therefore, there is no condition in `for`: it iterates until the `break` statement is reached on line [34] when the user presses `'n'`, as checked for on line [33].

During each iteration, on line [20], a new 0-valued grade is created, which is then overwritten on line [22] with a value entered by the user. If its value is correct, i.e. between 2.0 and 5.0, then on line [26] it is pushed to the end of the vector object `studentGradeVec` by a call of its `push_back` member function. The object and its member function are separated by a dot operator (`.`) – its syntax is presented in Section 3.9, as well as in the description of the *GROUP 2* operators (Table 3.15).
