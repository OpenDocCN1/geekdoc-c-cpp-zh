You can initialize a pointer to a function with the name of a function within the declaration of the pointer. The following is an example of this:

```
long sum(long num1, long num2);      // Function prototype
long (*pfun)(long, long) = sum;      // Pointer to function points to sum()
```

In general you can set the pfun pointer that you declared here to point to any function that accepts two arguments of type long and returns a value of type long. In the first instance you initialized it with the address of the sum() function that has the prototype given by the first statement.

Of course, you can also initialize a pointer to a function by using an assignment statement. Assuming the pointer pfun has been declared as above, you could set the value of the pointer to a different function with these statements:

```
long product(long, long);           // Function prototype
...

pfun = product;                     // Set pointer to function product ()
```

As with pointers to variables, you must ensure that a pointer to a function is initialized before you use it to call a function. Without initialization, catastrophic failure of your program is guaranteed.

# Try It Out   Pointers to Functions

To get a proper feel for these newfangled pointers and how they perform in action, try one out in a program.

```
// Ex6_01.cpp
// Exercising pointers to functions
#include <iostream>
using std::cout;
using std::endl;

long sum(long a, long b);             // Function prototype
long product(long a, long b);        // Function prototype

int main(void)
{
    long (*pdo_it)(long, long);      // Pointer to function declaration

    pdo_it = product;
    cout << endl
         << "3*5 = " << pdo_it(3, 5);   // Call product thru a pointer

    pdo_it = sum;                    // Reassign pointer to sum()
    cout << endl
         << "3*(4 + 5) + 6 = "
         << pdo_it(product(3, pdo_it(4, 5)), 6);   // Call thru a pointer,
                                                   // twice

    cout << endl;
    return 0;
```