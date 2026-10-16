
```
if (address == "STOP") break;

chopIPAddress(address, block1, block2, block3, block4);

cout << "The network/host blocks are:\n" << block1 << endl << block2 << endl << block3 << endl << block4 << endl;
}
```

```
/* Function to find the four network/host information blocks in a TCP/IP address.
Receive: TCP/IP address
Pass back: four network/host information blocks
Output: an error message if address is malformed
--------------------------------------------------------------------------*/
```

```
void chopIPAddress(const string & address, string & block1, string & block2, string & block3, string & block4)
{
int dot1 = address.find(".", 0);
assert(dot1 != string::npos);
block1 = address.substr(0, dot1);

int dot2 = address.find(".", dot1 + 1);
assert(dot2 != string::npos);
block2 = address.substr(dot1 + 1, dot2 - dot1 - 1);

int dot3 = address.find(".", dot2 + 1);
assert(dot3 != string::npos);
block3 = address.substr(dot2 + 1, dot3 - dot2 - 1);

assert(address.find(".", dot3 + 1) == string::npos);
block4 = address.substr(dot3 + 1, address.size() - dot3 - 1);
}
```

# SAMPLE RUNS:

Enter an IP address (STOP to quit): titan.ksc.nasa.gov
The network/host blocks are:
titan
ksc
nasa
gov

Enter an IP address (STOP to quit): 163.205.10.1
The network/host blocks are:
163
205
10
1

Enter an IP address (STOP to quit): STOP

## 10.4 SCOPE RULES

As we have seen, identifiers are used to name the objects and functions in a program. For example, a library might contain two summation functions, one to calculate sums of the form m + (m + 1) + (m + 2) + ... + (n - 1) + n, and another to calculate sums of the form 1 + 2 + ... + n. Although we might use different names for the functions, this is not necessary. We can name them both sum():

```
int sum(int n)
{
    return n * (n + 1) / 2;
}
```

```
int sum(int m, int n)
{
    assert(m <= n);
    return (n - m + 1) * (n + m) / 2;
}
```

As these definitions indicate

- 1. The same identifier can be used in different functions without conflict (e.g., parameter n).
- 2. Two functions can have the same name.

However, if we try to use the same identifier to define two different objects in the same function as in

```
void f()
{
    int value;
    ...
    char value;    // ERROR!
    ...
}
```

a compilation error results.

These examples raise an important question:

What rules govern the use of and/or access to an identifier?

As we shall see, some rules govern access to identifiers in general and other rules govern access to identifiers that are names of functions. In this section we describe these rules.

### 10.4.1 Scope: Identifier Accessibility

The scope of an identifier is that portion of a program where that identifier is the name of a constant, variable, or function that can be accessed. For example, consider again the definitions of the two summation functions. The identifier n is used in both definitions, but it

has two distinct scopes. In the first function, n is the name of the first parameter, and any uses of n in the body of that function refer to that parameter:

```
int sum (int n)
{
    return n * (n + 1) / 2;
}
```

```
int sum(int m, int n)
{
    assert(m <= n);
    return (n - m + 1) * (n + m) / 2;
}
```

In the second function, the identifier n is the name of the second parameter, and so any use of n in that function refers to it (and any use of parameter m in the function refers to itself).

> Any attempt to access an identifier outside its scope produces a compilation error.

For example, if we tried to use the value of the parameter n outside of these functions, an error message like

```
Identifier 'n' is undeclared
```

would be generated unless n is declared somewhere else and its scope includes this use of it. Understanding scope is important for understanding certain compilation errors.

Stated simply, the scope of an identifier depends on where the identifier is declared. The scopes of the identifiers we have seen thus far have been determined by four simple rules:

- S1. If an identifier is declared within a block, then its scope runs from its declaration to the end of the block.
- S2. If an identifier is a parameter of a function, then its scope is the body of the function.
- S3. If an identifier is declared in the initialization expression of a for loop, then its scope runs from its declaration to the end of the loop.
- S4. If an identifier is a declared outside all blocks and is not a parameter, then its scope runs from its declaration to the end of the file.

Note that an identifier's scope always begins at its declaration. One basic rule that follows from this is that an identifier must be declared before it can be used.

### 10.4.1.1 An Example

To illustrate how the compiler uses these scope rules, suppose that we were to rewrite the function getMenuChoice() from Section 9.2 as follows:

```
char getMenuChoice(const string &MENU, char firstChoice, char lastChoice)
{
    for (;;)
    {
    cout << MENU;
```

```
char choice;
cin >> choice;

if (choice >= firstChoice && choice <= lastChoice)
    break;

cerr << "\nI'm sorry, but " << choice
    << " is not a valid menu choice.\n";
}
return choice;        // ERROR!
}
```

When this function is compiled, the return statement generates an error message like

```
Identifier 'choice' is undeclared
```

(Before continuing, try to find the cause of the error using the scope rules.)

The problem is that by Scope Rule S1, the scope of choice only runs through the last statement of the block that is the body of the loop. Because the return statement appears after the block, it lies outside the scope of choice, and so the compiler generates an error when it attempts to access choice. The problem can be avoided by moving the declaration of choice to the outermost block of the function, thus ensuring that all statements that refer to choice lie within its scope:

```
char getMenuChoice(const string& MENU, char firstChoice, char lastChoice)
{
    char choice;
    for (;;)
    {
        cout << MENU;
        cin >> choice;

        if (choice >= firstChoice && choice <= lastChoice)
            break;

        cerr << "\nI'm sorry, but " << choice
            << " is not a valid menu choice.\n";
    }
    return choice;            // OK!
}
```

### 10.4.1.2 Objects Declared Outside All Blocks

Although we have not put any declarations of variables or constants outside all blocks, we have done so with prototypes of functions and with libraries that are included in a program. For example, in Example 10.5, the prototype of the function chopIPAddress() precedes the main function, so that the identifier chopIPAddress is declared outside all blocks. By Scope Rule S4, its scope thus extends from its declaration to the end of the file.

This is the reason why a function prototype must precede calls to that function. Because a prototype is a declaration of the function, it begins the scope of the function. Calls to that function later in the program thus lie within its scope.

Identifiers that are declared in a library's header file, such as cin, cout, cerr, and clog in iostream and the class string in the string library, are also governed by Scope Rule S4. When the compiler processes a #include directive outside all blocks as in

```
#include <iostream>
using namespace std;

int main()
{
...
}
```

all objects in that file are inserted outside all blocks and thus fall under Scope Rule S4. The scope of such declarations thus extends from their declarations (i.e., from the #include directive) to the end of the file.

### 10.4.1.3 Scopes of for-Loop Control Variables

Scope Rule S3 governs the scope of an identifier declared in the initialization expression of a for loop. To illustrate it, suppose that a program contains the statements

```
for (int i = 1; i <= someLimit; i++)
{
...
}

cout << "i = " << i << endl;        // ERROR
```

When the program is compiled, an error message like

```
Identifier 'i' is undeclared
```

results because Scope Rule S3 asserts that the scope of i ends at the bottom of the loop, so the output statement lies outside the scope of i. But this also means that i could be redeclared and used after the loop has ended. For example, it could be used in a later for loop,

```
for (int i = 1; i <= 100; i++)
{
...
}
...

for (int i = 50; i > 0; i--)
{
...
}
```
