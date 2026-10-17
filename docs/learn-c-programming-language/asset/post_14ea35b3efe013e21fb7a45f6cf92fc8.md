
By convention, if a pointer contains the null (zero) value, it is assumed to point to nothing.

To check for a null pointer you can use an if statement as follows:

```cpp
if(ptr)    // succeeds if p is not null

if(!ptr)   // succeeds if p is null
```

Thus, if all unused pointers are given the null value and you avoid the use of a null pointer, you can avoid the accidental misuse of an uninitialized pointer. Many times, uninitialized variables hold some junk values and it becomes difficult to debug the program.

## Pointer Arithmetic

As you understood, pointer is an address which is a numeric value; therefore, you can perform arithmetic operations on a pointer just as you can on a numeric value. There are four arithmetic operators that can be used on pointers: ++, --, +, and -

To understand pointer arithmetic, let us consider that **ptr** is an integer pointer which points to the address 1000. Assuming 32-bit integers, let us perform the following arithmetic operation on the pointer:

```cpp
ptr++
```

The **ptr** will point to the location 1004 because each time ptr is incremented, it will point to the next integer. This operation will move the pointer to the next memory location without impacting actual value at the memory location. If ptr points to a character whose address is 1000, then the above operation will point to the location 1001 because the next character will be available at 1001.

## Incrementing a Pointer

We prefer using a pointer in our program instead of an array because the variable pointer can be incremented, unlike the array name which cannot be incremented because it is a constant pointer. The following program increments the variable pointer to access each succeeding element of the array:

```cpp
#include <iostream>

using namespace std;

const int MAX = 3;

int main ()
{
    int var[MAX] = {10, 100, 200};
    int *ptr;

    // let us have array address in pointer.
    ptr = var;
    for (int i = 0; i < MAX; i++)
    {
        cout << "Address of var[" << i << "] = ";
        cout << ptr << endl;

        cout << "Value of var[" << i << "] = ";
        cout << *ptr << endl;

        // point to the next location
        ptr++;
    }
    return 0;
}
```

When the above code is compiled and executed, it produces result something as follows:

```text
Address of var[0] = 0xbfa088b0
Value of var[0] = 10
Address of var[1] = 0xbfa088b4
Value of var[1] = 100
Address of var[2] = 0xbfa088b8
Value of var[2] = 200
```

## Decrementing a Pointer

The same considerations apply to decrementing a pointer, which decreases its value by the number of bytes of its data type as shown below:

```cpp
#include <iostream>

using namespace std;

const int MAX = 3;

int main ()
{
    int var[MAX] = {10, 100, 200};
    int *ptr;

    // let us have address of the last element in pointer.
    ptr = &var[MAX-1];
    for (int i = MAX; i > 0; i--)
    {
        cout << "Address of var[" << i << "] = ";
        cout << ptr << endl;

        cout << "Value of var[" << i << "] = ";
        cout << *ptr << endl;

        // point to the previous location
        ptr--;
    }
    return 0;
}
```

When the above code is compiled and executed, it produces result something as follows:

```text
Address of var[3] = 0xbfdb70f8
Value of var[3] = 200
Address of var[2] = 0xbfdb70f4
Value of var[2] = 100
Address of var[1] = 0xbfdb70f0
Value of var[1] = 10
```

## Pointer Comparisons

Pointers may be compared by using relational operators, such as ==, <, and >. If p1 and p2 point to variables that are related to each other, such as elements of the same array, then p1 and p2 can be meaningfully compared.

The following program modifies the previous example by incrementing the variable pointer so long as the address to which it points is either less than or equal to the address of the last element of the array, which is &var[MAX - 1]:

```cpp
#include <iostream>

using namespace std;

const int MAX = 3;

int main ()
{
    int  var[MAX] = {10, 100, 200};
    int *ptr;

    // let us have address of the first element in pointer.
    ptr = var;
    int i = 0;
    while ( ptr <= &var[MAX - 1] )
    {
        cout << "Address of var[" << i << "] = ";
        cout << ptr << endl;

        cout << "Value of var[" << i << "] = ";
        cout << *ptr << endl;

        // point to the next location
        ptr++;
        i++;
    }
    return 0;
}
```

When the above code is compiled and executed, it produces result something as follows:

```text
Address of var[0] = 0xbfce42d0

Value of var[0] = 10

Address of var[1] = 0xbfce42d4

Value of var[1] = 100

Address of var[2] = 0xbfce42d8

Value of var[2] = 200
```

## Pointers vs Arrays

Pointers and arrays are strongly related. In fact, pointers and arrays are interchangeable in many cases. For example, a pointer that points to the beginning of an array can access that array by using either pointer arithmetic or array-style indexing. Consider the following program:

```cpp
#include <iostream>

using namespace std;

const int MAX = 3;

int main ()
{
    int var[MAX] = {10, 100, 200};
    int *ptr;

    // let us have array address in pointer.
    ptr = var;
    for (int i = 0; i < MAX; i++)
    {
        cout << "Address of var[" << i << "] = ";
        cout << ptr << endl;

        cout << "Value of var[" << i << "] = ";
        cout << *ptr << endl;

        // point to the next location
        ptr++;
    }
    return 0;
}
```

When the above code is compiled and executed, it produces result something as follows:

```text
Address of var[0] = 0xbfa088b0

Value of var[0] = 10

Address of var[1] = 0xbfa088b4

Value of var[1] = 100

Address of var[2] = 0xbfa088b8

Value of var[2] = 200
```

However, pointers and arrays are not completely interchangeable. For example, consider the following program:

```cpp
#include <iostream>

using namespace std;

const int MAX = 3;

int main ()
{
    int  var[MAX] = {10, 100, 200};

    for (int i = 0; i < MAX; i++)
    {
        *var = i;   // This is a correct syntax

        var++;      // This is incorrect.
    }
    return 0;
}
```

It is perfectly acceptable to apply the pointer operator * to var but it is illegal to modify var value. The reason for this is that var is a constant that points to the beginning of an array and can not be used as l-value.

Because an array name generates a pointer constant, it can still be used in pointer-style expressions, as long as it is not modified. For example, the following is a valid statement that assigns var[2] the value 500:

```cpp
*(var + 2) = 500;
```

Above statement is valid and will compile successfully because var is not changed.

## Array of Pointers

Before we understand the concept of array of pointers, let us consider the following example, which makes use of an array of 3 integers:

```cpp
#include <iostream>

using namespace std;

const int MAX = 3;

int main ()
{
    int  var[MAX] = {10, 100, 200};

    for (int i = 0; i < MAX; i++)
    {
        cout << "Value of var[" << i << "] = ";
        cout << var[i] << endl;
    }
    return 0;
}
```

When the above code is compiled and executed, it produces the following result:

```text
Value of var[0] = 10

Value of var[1] = 100

Value of var[2] = 200
```

There may be a situation, when we want to maintain an array, which can store pointers to an int or char or any other data type available. Following is the declaration of an array of pointers to an integer:

```cpp
int *ptr[MAX];
```

This declares ptr as an array of MAX integer pointers. Thus, each element in ptr, now holds a pointer to an int value. Following example makes use of three integers which will be stored in an array of pointers as follows:

```cpp
#include <iostream>
```

```cpp
char *names[MAX] = {
                "Zara Ali",
                "Hina Ali",
                "Nuha Ali",
                "Sara Ali",
};

for (int i = 0; i < MAX; i++)
{
    cout << "Value of names[" << i << "] = ";
    cout << names[i] << endl;
}
return 0;
}
```

When the above code is compiled and executed, it produces the following result:

```text
Value of names[0] = Zara Ali

Value of names[1] = Hina Ali

Value of names[2] = Nuha Ali

Value of names[3] = Sara Ali
```

## Pointer to a Pointer

A pointer to a pointer is a form of multiple indirection or a chain of pointers. Normally, a pointer contains the address of a variable. When we define a pointer to a pointer, the first pointer contains the address of the second pointer, which points to the location that contains the actual value as shown below.

![](img/7976f323fd1a5c8774f95fbf029a106f_139_0.png)

A variable that is a pointer to a pointer must be declared as such. This is done by placing an additional asterisk in front of its name. For example, following is the declaration to declare a pointer to a pointer of type int:

```cpp
int **var;
```
