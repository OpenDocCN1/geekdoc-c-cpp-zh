
- cout (pronounced "see out"): It is the standard output stream that is associated with the standard output device (monitor) and is used to display the output to users.
- cerr (pronounced "see err"): It is the standard error stream that is associated with the standard error device (monitor) and is used to report errors to the users. The cerr object does not have a buffer (temporary storage area) and hence, immediately reports errors to users.
- clog (pronounced "see log"): It is the buffered error stream that is associated with the standard error device (computer screen) and is used to report errors to users. Unlike cerr, clog reports errors to users only when the buffer is full.

For many years, C++ applied c-style headers, i.e., .h extension in the headers. However, the standard C++ library introduced new-style headers that include only header name. Hence, the most modern compilers do not require any extension, though they support the older .h extension. Some of C-style headers and their equivalent C++ style headers are listed in Table.

| Table C-style and C++ style headers |
| C-style header | C++ style header |
| --- | --- |
| <assert.h> | <cassert> |
| <ctype.h> | <cctype> |
| <float.h> | <float> |
| <limits.h> | <climits> |
| <math.h> | <cmath> |
| <stdio.h> | <cstdlib> |
| <string.h> | <cstring> |
| <iostream.h> | <iostream> |
| <iomanip.h> | <iomanip> |
| <fstream.h> | <fstream> |

# Namespace

Since its creation, C++ has gone through many changes by the C++ Standards Committee. One of the new features added to this namespace. A

## Object Oriented Concepts C++

namespace permits grouping of various entities like classes, objects, functions, and various C++ tokens, etc. under a single name. Different users can create separate namespaces and thus use similar names of entities. This avoids compile-time error that may exist due to identical-name conflicts.

The C++ Standards Committee has rearranged the entities of the standard library under a namespace called std. In Figure, the statement using namespace std informs the compiler to include all the entities present in the namespace std. The entities of a namespace can be accessed in different ways which are listed here.

- By specifying the using directive:

```cpp
using namespace std;
cout<<"Hello World";
```

- By specifying the full member name:

```cpp
std::cout<<"Hello World";
```

- By specifying the using declaration:

```cpp
using std::;
cout<<"Hello World";
```

As the new-style header is included, its contents are included in the std namespace. Thus, all the modern C++ compilers support these statements.

```cpp
#include<iostream>

using namespace std;
```

However, some old compilers may not support these statements. In that case, the statements are replaced by this single statement.

```cpp
#include<iostream.h>;
```

# main() Function

The main() is a start-up function that starts the execution of a C++ program. All C++ statements that need to be executed within main(). The compiler executes all the instructions written within the opening and closing braces '{' that enclose the body of main(). Once all the instructions in main() are executed, the control passes out of main(), terminating the entire program and returning a value to the operating system.

By default, main() in C++ returns an int value to the operating system. Therefore, main() should end with the return 0. A return value zero indicates success and a non-zero value indicates failure or error.

Below one is the sample Program of C++:

```cpp
// A Simple Program      -> This is a comment and ignored by the compiler
#include<iostream>    -> Header
#include<conio.h>      -> Header
Using namespace std      -> This tells the compiler to use std namespace
void main() {
    clrscr();
    int a,b;
    cout <<"Welcome To C++ Language";
    getch();
}
```

- 1. **#include**: In this, #include is the preprocessor directive that is given by the C++ language. It denotes to include the header file iostream.h means to include all the functions of the input-output stream header file which contains all the input and output functions like cout and cin. All these are contained in it.
- 2. **The Second Header file**: It is used for using the get and clrscr() functions.
- 3. **void main():** In this void means no Return of any value means a void doesn't return any value it just performs the executions of the program one by one.
- 4. **Main():** The () braces are the symbol of a function. Every function has braces. In this, Main() has a main role because the execution of all the programs are started from the Main() function This is also known as the starting point of the program. It executes the statements as they are in the Main() function and in the block means the open curly braces (and the closed curly braces).

These are used for denoting a block of statements that are to be executed.

## Object Oriented Concepts C++

- 5. Clrscr(): This is the built-in function that is provided by C++ for removing the results of the previous program which is made by any user. So, when a user will execute his program, this will first clear the contents of the screen.
- 6. **Console header file**: This function is used to clear the contents of the screen.
- 7. **getch():** This is the function is used for accepting a character from the user or it waits for a character from the user when a user press like a b c anything, then it will go to the program. So, the main thing is here is that the getch() function is for accepting and for waiting a character from the user.

# Storage Classes

Storage class of a variable defines the lifetime and visibility of a variable. Lifetime means the duration till the variable remains active and visibility defines in module of the variable is accessible. When we do not define a storage class, compiler automatically assigns a default storage class to it. A variable's storage class gives information about the **storage location of variable in memory, default initial value, scope of the variable and its lifetime**. There are five types of storage classes in C++. They are:

- 1. Automatic
- 2. External
- 3. Static
- 4. Register
- 5. Mutable

| Storage Class | Keyword | Lifetime | Visibility | Initial Value |
|---|---|---|---|---|
| Automatic | auto | Function Block | Local | Garbage |
| External | extern | Whole Program | Global | Zero |
| Static | static | Whole Program | Local | Zero |
| Register | register | Function Block | Local | Garbage |
| Mutable | mutable | Class | Local | Garbage |

C++ Storage Class

# Automatic Class

Automatic storage class assigns a variable to its default storage type. auto keyword is used to declare automatic variables. However, if a variable is declared without any keyword inside a function, it is automatic by default. This variable is visible only within the function it is declared and its lifetime is same as the lifetime of the function. Once the execution of function is finished, the variable is destroyed.

# Syntax of Automatic Class Declaration:

```cpp
datatype var_name [= value];
or
auto datatype var_name [= value];
```

 Example of Automatic Class:

```cpp
auto int x;
float y = 5.67;
```

# External Storage Class

External storage class assigns a reference to a global variable declared outside the program. extern keyword is used to declare external variables. They are visible throughout the program and its lifetime is same as the lifetime of the program where it is declared. This visible to all the functions present in the program.

# Syntax of External Storage Class Declaration:

```cpp
extern datatype var_name;
```

Example:

```cpp
extern float var1;
```

Examples of External Storage Class

Example 1: C++ program to create and use external storage.

```cpp
File: sub.cpp
int test=100;   // assigning value to test
void multiply(int n)
{
test=test*n;
}
```

```cpp
File: main.cpp
#include<iostream>
#include "sub.cpp" // includes the content of sub.cpp
using namespace std;
extern int test; // declaring test
int main()
{
    cout<<test<<endl;
    multiply(5);
    cout<<test<<endl;
    return 0;
}
```

**Note:** Run the main.cpp program

Output
100
500

# 3. Static Storage Class

Static storage class ensures a variable has the **visibility** mode of a local variable but **lifetime** of an external variable. It can be used only within the function where it is declared but destroyed only after the program execution has finished. When a function is called, the variable defined as static inside the function retains its previous value and operates on it. This is mostly used to save values in a recursive function.
