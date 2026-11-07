
## Program 16.24 A program with two customized manipulators

```cpp
{
ios.unsetf(ios::boolalpha);
return os;
}

int main()
{
    // Declaration and initialization of two boolean variables
    bool b1 = false;
    bool b2 = true;
    // Printing values of variables with alpha and noalpha manipulators
    cout << alpha << b1 << " " << b2 << endl;
    cout << noalpha << b1 << " " << b2 << endl;
    return 0;
}

Run:
false true
0 1
```

Knowing how to simulate a system manipulator helps us create our own manipulators. Assume we want to have a manipulator (with no arguments) called *currency* that prints values with $, followed by the leading asterisks to fill the beginning of the field and two decimal digits after the decimal point. Program 16.25 shows such a custom manipulator.

## Program 16.25 Creating and testing a customized manipulator

```cpp
/***************************************************************
 * A program that uses a customized manipulator                 *
 ***************************************************************/
#include <iostream>
#include <iomanip>
using namespace std;

ostream& currency(ostream& stream)
{
    stream << '$';
    stream.precision(2);
    stream.fill('*');
    stream.setf(ios::fixed, ios::floatfield);
    return stream;
}

int main()
{
    cout << currency << setw(12) << 12325.45 << endl;
    cout << currency << setw(12) << 0.36 << endl;
    return 0;
}

Run:
$*****12325.45
$********0.36
```

The values are printed as normally done on checks to fill the empty spaces with asterisks and thereby prevent someone from changing the check value.

## Manipulator with Arguments

Simulation of manipulators with arguments is a little more involved. A pointer to function cannot have an argument. In other words, we cannot have a pointer to a function with a parameter, such as `setw(4)`; the pointer can only be named `setw`. This means we must change our strategy. Instead of a pointer to function, we can consider the phrase `setw(4)` as a call to a constructor of a class with only one data member of type integer. In other words, we interpret the statement

```cpp
cout << setw(4);
```

as an operator with two operands. The first operand is an instance of type `ostream`; the second is an instance of type `setw`. Now we can create a manipulator with an argument using the following steps:

- 1. We need a class whose name is the same as the name of the manipulator and with one data member of the same type as the type of manipulator argument.
- 2. We need to overload the insertion or extraction operator for the class in which the first parameter is of type stream (`ostream` or `istream`) and the second parameter is the same as the class in step 1.
- 3. In the body of the overloaded operator, we code the action to achieve the purpose of the manipulator.

> A manipulator with an argument can be created by defining
> a class with one data member in which the insertion
> or extraction operator is overloaded.

We simulate the manipulator `setw(n)`, but we call it `length(n)` so it will be treated as a new manipulator. Program 16.26 shows the interface for the class `length` (we use a lowercase letter for the name of the class for consistency with the manipulator).

## Program 16.26 The interface file (length.h)

```cpp
/**************************************************************
 * Interface file for a class named length                    *
 **************************************************************/
#ifndef LENGTH_H
#define LENGTH_H
#include <iostream>
using namespace std;

class length
{
private:
    int n;
public:
    length(int n);
    friend ostream& operator<<(ostream& stream, const length& len);
};
#endif
```

We also implement the class length as shown in Program 16.27. Note that we want the operator << to set the width formatting variable with the value of data member n in the class length.

We write Program 16.28 to apply the new manipulator and test it.

## Program 16.27 The implementation file (length.cpp)

```cpp
/**************************************************************
 * Implementation of the class length                         *
 **************************************************************/
#include "length.h"

// Definition of the length member function
length::length(int n1)
: n(n1)
{
}

// Overloaded operator <<
ostream& operator<<(ostream& stream, const length& len)
{
    stream.width(len.n);
    return stream;
}
```

## Program 16.28 The application file (application.cpp)

```cpp
/**************************************************************
 * An application program to use the manipulator length(n)     *
 **************************************************************/
#include "length.h"

int main()
{
    cout << length(10) << 123 << endl;
    cout << length(20) << 234 << endl;
    return 0;
}

Run:
    123
    234
```

## 16.6 PROGRAM DESIGN

In this section we design three programs to show the applications of the input/output streams.

### 16.6.1 Merging Two Sorted Files

We want to create a merge sort on two files of integers. Assume we have two files of integers in which the integers are sorted (arranged from the smallest to the largest). We want to merge the two files to create a new file in which the integers are still sorted and any duplicates are maintained. Figure 16.15 shows the contents of infile1, infile2, and outfile.

![](img/d68f6199646ca63591a6d8419e0ed4ba_784_0.png)

**Note:**
There is only one variable named *first* and one named *second*, but their values and conditions change as the sort progresses.

**Figure 16.15.** Data flow in a merge sort.

The process of merging these files takes 13 iterations. In each iteration, either the contents of variable *first* or variable *second*, but not both, is moved to the outfile. Some integers remain in the corresponding variable for a few iterations before they can move to the output file. Note that the comparison and the decision to move an integer to the output file is always based on the contents of the variables *first* and *second*.

Program 16.29 shows the code. In line 14 we declare two variables, *first* and *second*, to hold an integer of the first and second input files during processing. In line 15 we create a sentinel (a very large integer, as we learned in previous chapters).

## Program 16.29 Merge sort process applied to two files

```cpp
/************************************************************/
/* A program to merge two files of sorted integer to create  */
/* a file of sorted integers                                */
/************************************************************/
#include <iostream>
#include <fstream>
#include <assert.h>
#include <limits>
using namespace std;

int main()
{
    // Declaration and Initialization
    int first, second;
    int sentinel = numeric_limits<int>::max();
    // Instantiating streams and opening files
    ifstream strm1("infile1");
    ifstream strm2("infile2");
    ofstream strm3("outfile");
    if (!strm1.is_open())
    {
        cout << "Error opening infile1!" << endl;
        assert(false);
    }
    if (!strm2.is_open())
    {
        cout << "Error opening infile2!" << endl;
        assert(false);
    }
    if (!strm3.is_open())
    {
        cout << "Error opening outfile!" << endl;
        assert(false);
    }
    // Processing
36    strm1 >> first;
37    strm2 >> second;
38    while (strm1 || strm2)
39    {
40        if (first <= second)
41        {
42            strm3 << first << " ";
43            strm1 >> first;
44            if (!strm1)
45            {
46                first = sentinel;
47            }
48        }
49        else
50        {
51            strm3 << second << " ";
52            strm2 >> second;
53            if (!strm2)
54            {
55                second = sentinel;
56            }
57        }
58    }
59    // Closing files
60    strm1.close();
61    strm2.close();
62    strm3.close();
63    return 0;
64 }
```

### 16.6.2 Symmetric Ciphers

Transmission of information using files must be handled in a secure way. One of the common techniques used for this purpose is cryptography. **Cryptography**, a word with Greek origins, means “secret writing.” It involves two distinct mechanisms: symmetric-key and asymmetric-key cryptography. Cryptography uses keys to change an original message, called *plaintext*, to a secret message, called *ciphertext*.

There are two broad categories of cryptography: *symmetric* and *asymmetric*. We discuss and use an example of the first in this section; we use an example of the second in the next section.

In *symmetric-key cryptography* we use the same key for both encryption and decryption. The key can be used for bidirectional communication, which is why it is called *symmetric*. Figure 16.16 shows the general idea behind a symmetric-key cipher.

In Figure 16.16, an entity, Alice, sends a message to another entity, Bob, over an insecure channel with the assumption that an adversary cannot understand the contents of the message by simply eavesdropping over the channel.
