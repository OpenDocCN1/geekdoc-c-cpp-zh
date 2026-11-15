Declaration of Pointer Types: Pointer types are declared using type declaration statements and the pointer operator (*). Pointer types can be initialized using the address operator (&).

Syntax: Declaration of a pointer
type *identifier[=&identifier];

Example: Declare two pointers to int
int *iPtr, *jPtr;

Example: Declare and initialize a pointer to int
int a=5;
int *aPtr = &a;

We now extend program chapter9_1 to demonstrate the relationship between objects, addresses, and pointers. Consider the following program:

```
/*-----------------------------------------------------*/
/* Program chapter9_3 */
/* */
/* This program demonstrates the relationship */
/* between objects, addresses, and pointers. */
/*-----------------------------------------------------*/
#include <iostream> //Required for cout
using namespace std;
int main()
{
// Declare and initialize objects.
int a(1), b(2), *ptr(&a);

// Print addresses and contents of all objects.
cout << "a = " << a << "; address of a = " << &a << endl;
cout << "b = " << b << "; address of b = " << &b << endl;
cout << "ptr = " << ptr << "; address of ptr = " << &ptr << endl;
cout << "ptr points to the value " << *ptr << endl;
return 0;
}
/*-----------------------------------------------------*/
```

A sample output from this program is the following:

```
a = 1; address of a 0xbffff8d8
b = 2; address of b 0xbffff8d4
ptr = 0xbffff8d8; address of ptr 0xbffff8d0
ptr points to the value 1
```

Note that the values of the pointer to a and the address of a are the same.