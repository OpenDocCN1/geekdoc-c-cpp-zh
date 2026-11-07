
The program in Example E-2 created the binary file `customer.dat` consisting of certain customers’ data. You can use the function `seekg` to move the reading position of this file to any record. Suppose `inFile` is an `ifstream` object used to open the binary file `customer.dat`.

The following statement calculates the size of a `customerType` struct and stores it in the variable `custSize`:

```cpp
long custSize = sizeof(cust);
```

We can use the value of the variable `custSize` to move the reading position to a specific record in the file. For example, consider the following statement:

```cpp
inFile.seekg(6 * custSize, ios::beg);
```

This statement moves the reading position just after the sixth customer’s record, that is, just before the seventh customer’s record.

The following program further illustrates how the function `seekg` works with structs.

## EXAMPLE E-6

```cpp
//Reading a file randomly

#include <iostream>
#include <fstream>
#include <iomanip>

using namespace std;

struct customerType
{
    char firstName[15];
    char lastName[15];
    int ID;
    double balance;
};

void printCustData(const customerType& customer);

int main()
{
    customerType cust;                         //Line 1
    ifstream inFile;                            //Line 2

    long custSize = sizeof(cust);               //Line 3

    inFile.open("customer.dat", ios::binary);  //Line 4
    if (!inFile)                                //Line 5
    {
        cout << "The input file does not exist. "
             << "The program terminates!!!!" << endl;  //Line 6
        return 1;                                      //Line 7
    }

    cout << fixed << showpoint << setprecision(2);     //Line 8

    //randomly read the records and output them
    inFile.seekg(6 * custSize, ios::beg);              //Line 9
    inFile.read(reinterpret_cast<char *> (&cust),
                sizeof(cust));                         //Line 10

    cout << "Seventh customer's data: " << endl;       //Line 11
    printCustData(cust);                                //Line 12

    inFile.seekg(8 * custSize, ios::beg);              //Line 13
    inFile.read(reinterpret_cast<char *> (&cust),
                sizeof(cust));                         //Line 14

    cout << "Ninth customer's data: " << endl;         //Line 15
    printCustData(cust);

    inFile.seekg(-8 * custSize, ios::end);             //Line 16
    inFile.read(reinterpret_cast<char *> (&cust),
                sizeof(cust));                         //Line 17
    cout << "Eighth (from the end) customer's data: "
         << endl;                                      //Line 18
    printCustData(cust);                               //Line 19

    inFile.close();        //close the file            //Line 20

    return 0;                                          //Line 21
}

void printCustData(const customerType& customer)
{
    cout << "   ID: " << customer.ID << endl
         << "   First Name: " << customer.firstName << endl
         << "   Last Name: " << customer.lastName << endl
         << "   Account Balance: $" << customer.balance
         << endl;
}
```

### Sample Run:

```text
Seventh customer's data:
   ID: 22222
   First Name: Jose
   Last Name: Ramey
   Account Balance: $25345.35
Ninth customer's data:
   ID: 55555
   First Name: Tommy
   Last Name: Pitts
```

```cpp
//read the data at location 0 in the file
inFile.read(reinterpret_cast<char *> (&st),
            sizeof(st));                         //Line 24

while (inFile)                                  //Line 25
{
    if (st.ID != 0)                              //Line 26
        printStudentData(st);                    //Line 27

    //read the data at the current reading position
    inFile.read(reinterpret_cast<char *> (&st),
               sizeof(st));                      //Line 28
};

return 0;                                        //Line 29
}

void printStudentData(const studentType& student)
{
    cout << left << setw(3) << student.ID
         << setw(16) << student.FirstName
         << setw(16) << student.LastName
         << right << setw(10)<< student.GPA
         << endl;
}
```

### Sample Run:

| ID | First Name | Last Name | Current GPA |
|---:|---|---|---:|
| 2 | Sheila | Duffy | 4.00 |
| 10 | Ajay | Kumar | 3.60 |
| 12 | Ashley | White | 3.90 |
| 16 | Tommy | Pitts | 2.40 |
| 23 | Rita | Gupta | 3.40 |
| 34 | Brad | Smith | 3.50 |
| 36 | Salma | Quade | 3.90 |
| 41 | Steve | Sharma | 3.10 |
| 45 | Sheila | Robinson | 2.50 |
| 56 | Lisa | Johnson | 2.90 |
| 67 | Jose | Ramey | 3.80 |
| 75 | Jennifer | Ackerman | 4.00 |

The data in the file studentData.txt is as follows:

```text
12 Ashley White 3.9
34 Brad Smith 3.5
56 Lisa Johnson 2.9
45 Sheila Robinson 2.5
23 Rita Gupta 3.4
10 Ajay Kumar 3.6
67 Jose Ramey 3.8
2 Sheila Duffy 4.0
16 Tommy Pitts 2.4
36 Salma Quade 3.9
75 Jennifer Ackerman 4.0
41 Steve Sharma 3.5
```

## Naming Conventions of Header Files in ANSI/ISO Standard C++ and Standard C++

The programs in this book are written using ANSI/ISO Standard C++. As indicated in Chapter 1, there are two versions of C++—ANSI/ISO Standard C++ and Standard C++. For the most part, these two standards are the same. The header files in Standard C++ have the extension .h, while the header files in ANSI/ISO Standard C++ have no extension. Moreover, the names of certain header files, such as math.h, in ANSI/ISO Standard C++ start with the letter c. The language C++ evolved from C. Therefore, certain header files—such as math.h, stdlib.h, and string.h—were brought from C into C++. The header files—such as iostream.h, iomanip.h, and fstream.h—were specially designed for C++. Recall that when a header file is included in a program, the global identifiers of the header file also become the global identifiers of the program. In ANSI/ISO Standard C++, to take advantage of the namespace mechanism, all of the header files were modified so that the identifiers are declared within a namespace. Recall that the name of this namespace is std.

In ANSI/ISO Standard C++, the extension .h of the header files that were specially designed for C++ was dropped. For the header files that were brought from C into C++, the extension .h was dropped and the names of these header files start with the letter c. Following are the names of the most commonly used header files in Standard C++ and ANSI/ISO Standard C++:

| Standard C++ Header File Name | ANSI/ISO Standard C++ Header File Name |
|---|---|
| assert.h | cassert |
| ctype.h | cctype |
| float.h | cfloat |
| fstream.h | fstream |
| iomanip.h | iomanip |
| iostream.h | iostream |
| limits.h | climits |
| math.h | cmath |
| stdlib.h | cstdlib |
| string.h | cstring |

To include a header file, say, `iostream`, the following statement is required:

```cpp
#include <iostream>
```

Furthermore, to use identifiers, such as `cin`, `cout`, `endl`, and so on, the program should use either the statement:

```cpp
using namespace std;
```

or the prefix `std::` before the identifier.

*This page intentionally left blank*

The C++ standard library contains many predefined functions, named constants, and specialized data types. This appendix discusses some of the most widely used library routines (and several named constants). For additional explanation and information on functions, named constants, and so on, check your system documentation. The names of the Standard C++ header files are shown in parentheses.

## Header File `cassert` (`assert.h`)

The following table describes the function assert. Its specification is contained in the header file cassert (assert.h).

| Function | Description | Details |
|---|---|---|
| `assert(expression)` | expression is any `int` expression; expression is usually a logical expression | - If the value of expression is nonzero (`true`), the program continues to execute.<br>- If the value of expression is 0 (`false`), execution of the program terminates immediately. The expression, the name of the file containing the source code, and the line number in the source code are displayed. |

> **NOTE:** To disable all of the `assert` statements, place the preprocessor directive `#define NDEBUG` before the directive `#include <cassert>`.
