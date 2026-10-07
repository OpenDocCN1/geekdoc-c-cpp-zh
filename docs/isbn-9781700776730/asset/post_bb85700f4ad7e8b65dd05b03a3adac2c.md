
Don't worry yet about the syntax, but we use the scope resolution operator here to identify which foo() function we're giving definition to. One way to view the scope resolution operator is to view it as providing a path to an identifier. More later!

# Structures

In C, structure names are not type names. The word struct must be used whenever the structure is referred to:

```
struct Employee {
  int salary;
  struct Employee *reportsTo;
}
struct Employee Haley;
struct Employee* updateReportsTo(struct Employee*, struct Employee*);
```

In C++, structure names are type names, just as if they were typedef'd. The structure keyword is superfluous:

```cpp
struct Employee {
  int salary;
  Employee *reportsTo;
}
Employee Haley;
Employee* updateReportsTo(Employee*, Employee*);
```

# Operator Precedence

In the following table of operator precedence, C++ operators are divided into 13 categories. The #1 category has the highest precedence, category #2 (Unary operators) takes second precedence, and so on to the Comma operator, which has lowest precedence. The operators within each category have equal precedence. The Unary (category #2), Conditional (category #11), and Assignment (category #12) operators associate right-to-left; all other operators associate left-to-right.

| # | Category | Operator | What it is (or does) |
|---|---|---|--|
| 1 | Highest | () | Function call |
| | | [] | Array subscript |
| | | -> | C++ indirect component selector |
| | | :: | C++ scope access/resolution |
| | | | | C++ direct component selector |
| 2 | Unary | ! | Logical negation (NOT) |
| | | ~ | Bitwise (1's) complement |
| | | + | Unary plus |
| | | - | Unary minus |
| | | ++ | Preincrement or postincrement |
| | | -- | Predecrement or postdecrement |
| | | & | Address |
| | | * | Induction |
| | | sizeof | returns size of operand, in bytes |
| | | new | dynamically allocates C++ storage |
| | | delete | dynamically deallocates C++ storage |
| 3 | Member access | * | C++ dereference |
| | | ->* | C++ dereference |
| 4 | Multiplicative | *, /, % | Multiply / Divide / Remainder (modulus) |
| 5 | Additive | +, - | Binary plus / Binary minus |
| 6 | Shift | <<, >> | Shift left / Shift right |
| 7 | Relational | <, <=, >, >= | Less than / Less than or equal to / Greater than / Greater than or equal to |
| 8 | Equality | =, != | Equal to / Not equal to |
| 9 | Bitwise | &, |, ^ | | Bitwise AND / Bitwise OR / Bitwise XOR |
| 10 | Logical | &&, || | Logical AND / Logical OR |
| 11 | Conditional | ? | Conditional |
| 12 | Assignment = =, *,, /, %, += | Simple assignment / Assign product / Assign quotient / Assign remainder (modulus) / Assign sum |
| | | -= | Assign difference |
| | | &= | Assign bitwise AND |
| | | ^= | Assign bitwise XOR |
| | | |= | Assign bitwise OR |
| | | <<= | Assign left shift |
| | | >>= | Assign right shift |
| 13 | Comma | , | Evaluate |

All of the operators in this can be overloaded except the following:

- * C++ direct component selector
- * C++ dereference
- :: C++ scope access/resolution
- ? : Conditional

# C++ I/O Tutorial

# First C++ Program

This exercise is intended to make sure you can get your C++ compiler to work and to demonstrate a few simple features of the C++ I/O system. When you want to send output to the standard output device in a C++ program, you can use one of the output-related functions from the standard C++ library. For example, the line:

```cpp
printf("String = %s\n", buf);
```

displays the value of the string buf on the standard output device. However, since we are using C++ code, we use cout from the ostream class to send output to the standard output device. For example, the line:

```cpp
cout << "String = " << buf << '\n';
```

displays the same string buf on the standard output device. Type in, compile and execute the source code for the following C++ program:

```cpp
// test.cpp - simple i/o test program

#include <iostream>

using namespace std;

int main() {
    char buf[80];

    cout << "Type your first name: ";
    cin >> buf;
    cout << "Congratulations, " << buf << ", you have successfully compiled a C++ program.\n";
    return 0;
}
```

In this program, cin and cout are input and output objects, and the << and >> operators, which normally do bit-shifts in C, have been overloaded to mean get from (insertion) and put to (extraction). All of this is handled in the standard C++ I/O library, iostream. Note that C++ program files have the suffix .cpp.

Now, comment out the preprocessor directive:

```cpp
// #include <iostream>
```

and compile the C++ program. Note the error messages that result.

# Output Streams

While you can use printf() or cout, using both of them in the same program can lead to problems. To see the problems that could arise, type in, compile and execute the following C++ program:

```cpp
// bad.cpp - uses both printf() and cout to send output to the
// standard output device

#include <iostream>
#include <stdio.h>

using namespace std;

int main() {
    // turn off buffered output for cout
    cout.unset(ios::unitbuf);

    printf("Print this first.\n");
    cout << "Print this second.\n";
    printf("Print this third.\n");
    cout << "Print this last.\n";
    return 0;
}
```

Looking closely at bad.cpp we can see we've alternately printf() and cout to display four strings. At first glance, the code in bad.cpp appears to have no bugs. However, some older C++ compilers will produce the following output:

Print this first.
Print this third.
Print this second.
Print this last.

while newer C++ compilers will produce the following output:

Print this first.
Print this second.
Print this third.
Print this last.

Note: For the sake of learning some important elements of output streams, we're going to focus on what's happening. Actually, bad.cpp doesn't produce the output we'd expect. Because cout uses buffered output, it doesn't display the strings until the buffer is full or the program terminates. Since printf() calls immediately displays. Next, bad.cpp inserts the string Print this second. Second is still in cout's buffer. Finally, bad.cpp inserts the string Print this last. into cout, which also stores in memory. When bad.cpp terminates, it calls the destructor for cout, which automatically flushes any-empty buffers.

Fortunately, there is a way you can force cout to flush the contents of its buffer. (Note that the ability to flush a buffer's output is a very important task in working with output streams.) The ostream class defines the flush() member function, which you can call whenever you'd like. The ofstream class also defines the flush manipulator, which you can insert along with other data in the output stream. The following program ok.cpp uses the flush manipulator to force the display of the strings it inserts into cout.

```cpp
// ok1.cpp - uses flush with cout

#include <iostream>
#include <stdio.h>

using namespace std;

int main() {
    // turn off buffered output for cout
    cout.unsetf(ios::unitbuf);

    printf("Print this first.\n");
    cout << "Print this second.\n" << flush;
    printf("Print this third.\n");
    cout << "Print this last.\n" << flush;
    return 0;
}
```

As you can see, you simply insert the flush manipulator whenever you want cout to flush the contents of the buffer. When you compile and run ok1.cpp, you get the output you'd expect on all compilers.

Instead of inserting the flush manipulator after each output string, we could have added a new line that calls the ostream::flush() member function. For example, the line:

```cpp
cout.flush();
```

flushes cout's buffer directly.
