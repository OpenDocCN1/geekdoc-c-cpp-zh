
The following memory snapshot shows the contents of the two memory locations at the time the cout statements are executed. This memory snapshot also shows the memory address of each of the variables.

```
int a [0xbfff8d8] [1]
int b [0xbfff8d4] [2]
```

We do not usually indicate the memory addresses in these diagrams because the addresses used are system dependent and change with every run of the program.

In the next example, which is a modification to the previous program, there are no initial values given to objects a and b:

```
/**
 * Program chapter9_2
 *
 * This program demonstrates the relationship
 * between objects and addresses.
 */
#include <iostream>//Required for cout
using namespace std;
int main()
{
   // Declare and initialize objects.
   // int a, b;

   // Print the contents and addresses of a and b.
   cout << "a= " << a << " address of a = " << &a << endl;
   cout << "b= " << b << " address of b = " << &b << endl;

   return 0;
}
```

A sample output from this program is the following:

```
a = -1073743608; address of a = 0xbffff8e8
b = 1073784016; address of b = 0xbffff8e4
```

A memory snapshot at the time the cout statements are executed shows a question mark for the contents of the memory locations because the variables have not been initialized. However, memory has been allocated for the variables, thus the memory addresses for each of the variables has been established.

```
int a [0xbfff8e8] [?]
int b [0xbfff8e4] [?]
```

While we see that there are values in the variables, even though we have not assigned any in the program, we should not assume anything about these values. This example illustrates the importance of being sure that a program initializes an object before using its value in other statements in a program.

- 1. Run program chapter9_1 two times on the computer that you are using for class assignments. Did your computer use the same addresses or different addresses? Compare the results with your classmates.
- 2. Run program chapter9_2 presented in this section. What values were in the locations assigned to a and b? Do the values change from one execution of the program to another?

## Pointer Assignment

pointer

The C++ language allows us to store the address of a memory location in a special type of object called a pointer. When a pointer is defined, the type of object to which it will point must also be defined. The type of object to which a pointer will point is referred to as the pointer's base type. The base type of a pointer determines how the object being pointed to will be interpreted. Thus, a pointer defined to point to an integer object cannot also be used to point to a floating-point object. The following statement declares two integer objects and a pointer to an integer object. Note that an asterisk is used to indicate that the object is a pointer; this asterisk is also called a dereference or indirection operator:

base type

dereference indirection

```
int a, b, *ptr;
```

This statement specifies that memory addresses should be assigned to three objects—two integer objects and a pointer to an integer object. The statement does not specify the initial values for a, b, and ptr. Thus, the memory snapshot after this declaration indicates that the initial contents of all objects are not specified. The diagram uses an arrow, and a question mark, to indicate that ptr is a pointer, and that what ptr points to has not been specified:

```
int a [?]
int b [?]
int* ptr [?] ->
```

To specify that ptr should point to the object a, we could use an assignment statement that stores the address of a in ptr:

```
int a, b, *ptr;
ptr = &a;
```

We could have initialized ptr in the declaration statement:

```
int a, b, *ptr=&a;
```

In either case, the memory snapshot after the declaration is the following:

```
int* ptr [box]
int a [?]   int b [?]
```

Note that it is not necessary to show the contents of ptr, as long as the object to which it points is specified.

Consider this set of statements:

```
// Declare and initialize objects.
int a, b, *ptr(&a);
...
// Assign the value pointed to by ptr to b.
b = *ptr;
```

This last statement is read as “b is assigned the value at the address contained in ptr,” or “b is assigned the value pointed to by ptr.” The memory snapshot before the assignment statement is executed is the following:

```
int* ptr [ ]
     |
int a [5]   int b [9]
```

The memory snapshot after the assignment statement is executed is the following:

```
int* ptr [ ]
     |
int a [5]   int b [5]
```

Thus, b is assigned the value pointed to by ptr. Now consider this set of statements:

```
// Declare and initialize objects.
int a, b, *ptr(&a);
...
// Assign the value of b to the object
// pointed to by ptr.
*ptr = b;
```

The assignment statement in this set of statements is read “what is pointed to by ptr is assigned the value of b.” The memory snapshot before the assignment statement is executed is the following:

```
int* ptr [ ]
     |
int a [5]   int b [9]
```

The memory snapshot after the assignment statement is executed is the following:

```
int* ptr [ ]
     |
int a [9]   int b [9]
```

Thus, the value pointed to by ptr is assigned the value in b.

## Statement Box 9.1 Declaration of Pointer Types: Pointer types are declared using type declaration statements and the pointer operator (*). Pointer types can be initialized using the address operator (&).

Syntax: Declaration of a pointer
type * identifier[=&identifier];

Example: Declare two pointers to int
int *iPtr, *jPtr;

Example: Declare and initialize a pointer to int
int a;
int *aPtr = &a;

We now extend program chapter9_1 to demonstrate the relationship between objects, addresses, and pointers. Consider the following program:

```
/*
 * Program chapter9_3
 *
 * This program demonstrates the relationship
 * between objects, addresses, and pointers.
 */

#include <iostream> //Required for cout
using namespace std;
int main()
{
    // Declare and initialize objects.
    int a, b, *ptr(&a);

    // Print address and contents of all objects.
    cout << "a = " << a << "; address of a = " << &a << endl;
    cout << "b = " << b << "; address of b = " << &b << endl;
    cout << "ptr = " << ptr << "; address of ptr = " << &ptr << endl;
    cout << "*ptr points to the value " << *ptr << endl;

    return 0;
}
/*--------------------------------------*/
```

A sample output from this program is the following:

```
a = 1; address of a = 0xbffffff8d
b = 2; address of b = 0xbffffff84
ptr = 0xbffffff8d; address of ptr = 0xbffffff80
ptr points to the value 1
```

Note that the values of the pointer to a and the address of a are the same.

## Practice 9.1

Give memory snapshots after each of these sets of statements are executed.

- 1. int a, b, *ptr;
   ptr = &b;
   
- 2. int a, b, *ptr=&b;
   a = *ptr;
   
- 3. int a, b, c, *ptr=&c;
   b = *ptr;
   *ptr = a;
   
- 4. int a, b, c, *ptr;
   ptr = &c;
   c = b;
   a = *ptr;

## Pointer Arithmetic

The operations that can be performed with pointers (or addresses) are limited to the following:

- A pointer can be assigned to another pointer of the same type
- An integer value can be added to or subtracted from a pointer
- A pointer can be assigned or compared to the literal `nullptr`

In addition, pointers to elements of the same array can be subtracted or compared as a means to accessing elements in the array.

A pointer can point to only one location at a time, but several pointers can point to the same location, as illustrated in this next example. Both `ptr_1` and `ptr_2` point to the same object after the following statements are executed:

```
// Declare and initialize objects.
int x(-5), y(8), *ptr_1, *ptr_2;
...
// Assign both pointers to x.
ptr_1 = &x;
ptr_2 = ptr_1;
```

The memory snapshot after these statements are executed is

![](img/0235a4ea835dc4575bd036e024a533b3_509_0.png)
