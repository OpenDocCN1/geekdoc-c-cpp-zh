
### EXAMPLE 14-9

```cpp
// Handling bad_alloc exception thrown by the operator new.

#include <iostream>           //Line 1

using namespace std;          //Line 2

int main()                    //Line 3
{                             //Line 4
    int *list[100];           //Line 5

    try                       //Line 6
    {                         //Line 7
        for (int i = 0; i < 100; i++) //Line 8
        {                     //Line 9
            list[i] = new int[50000000]; //Line 10
            cout << "Line 11: Created list[" << i
                 << "] of 50000000 components." //Line 11
                 << endl;         //Line 12
        }                     //Line 13
    }                         //Line 14
    catch (bad_alloc be)      //Line 15
    {                         //Line 16
        cout << "Line 16: In the bad_alloc catch "
             << "block: " << be.what() << "." //Line 16
             << endl;         //Line 17
    }                         //Line 18

    return 0;                 //Line 19
}                             //Line 19
```

**Sample Run:**

```text
Line 11: Created list[0] of 50000000 components.
Line 11: Created list[1] of 50000000 components.
Line 11: Created list[2] of 50000000 components.
Line 11: Created list[3] of 50000000 components.
Line 11: Created list[4] of 50000000 components.
Line 11: Created list[5] of 50000000 components.
Line 11: Created list[6] of 50000000 components.
Line 11: Created list[7] of 50000000 components.
Line 16: In the bad_alloc catch block: bad allocation.
```

The preceding program works as follows. The statement in Line 5 declares list to be an array of 100 pointers. The body of the for loop in Line 8 is designed to execute 100 times. For each iteration of the for loop, the statement in Line 10 uses the operator new to allocate an array of 50000000 components of type int. As shown in the sample run, the operator new is able to create eight arrays of 50000000 components each. In the ninth iteration, the operator new is unable to create the array and throws a `bad_alloc` exception.

This exception is caught and processed by the `catch` block in Line 14. Notice that the expression `be.what()` returns the string `bad allocation`. (Moreover, the string returned by `be.what()` is IDE dependent. Some IDEs might return the string `bad_alloc`.) After the statement in Line 16 executes, control exits the `try/catch` block, and the statement in Line 18 terminates the program.

## Creating Your Own Exception Classes

![](img/b217c421655b51e7494cf3b89bb5432d_1072_0.png)

Whenever you create your own classes or write programs, exceptions are likely to occur. As you have seen, C++ provides numerous exception classes to deal with these situations. However, it does not provide all of the exception classes you will ever need. Therefore, C++ enables programmers to create their own exception classes to handle both the exceptions not covered by C++'s exception classes and their own exceptions. This section describes how to create your own exception classes.

C++ uses the same mechanism to process the exceptions that you define as it uses for built-in exceptions. However, you must throw your own exceptions using the `throw` statement.

In C++, any class can be considered an exception class. Therefore, an exception class is simply a class. It need not be inherited from the `class exception`. What makes a class an exception is how you use it.

The exception class that you define can be very simple in the sense that it does not contain any members. For example, the following code can be considered an exception class:

```cpp
class dummyExceptionClass
{
};
```

The program in Example 14-10 uses a user-defined class (with no members) to throw an exception.

### EXAMPLE 14-10

```cpp
// Using a user-defined exception class.

#include <iostream>                  //Line 1

using namespace std;                 //Line 2

class divByZero                      //Line 3
{};                                  //Line 4

int main()                           //Line 5
{                                    //Line 6
    int dividend, divisor, quotient; //Line 7
```

The exception class `divByZero` designed and used in Example 14-10 has no members. Next, we illustrate how to create exception classes with members.

If you want to include members in your exception class, you typically include constructors and the function `what`. Consider the following definition of the `class divisionByZero`.

```cpp
// User-defined exception class.

#include <iostream>                         //Line 1
#include <string>                           //Line 2

using namespace std;                        //Line 3

class divisionByZero                        //Line 4
{
public:                                     //Line 6
    divisionByZero()                        //Line 7
    {
        message = "Division by zero";      //Line 9
    }

    divisionByZero(string str)              //Line 11
    {
        message = str;                      //Line 13
    }

    string what()                           //Line 15
    {
        return message;                     //Line 17
    }

private:                                    //Line 19
    string message;                         //Line 20
};                                          //Line 21
```

The definition of the `class divisionByZero` contains two constructors: the default constructor and the constructor with parameters. The default constructor stores the string "Division by zero" in an object. The constructor with parameters allows users to create their own error messages. The function `what` is used to return the string stored in the object.

> **NOTE**
>
> In the definition of the `class divisionByZero`, the constructors can also be written as:
>
> ```cpp
> divisionByZero() : message("Division by zero"){}
> divisionByZero(string str) : message(str){}
> ```

The program in Example 14-11 uses the preceding class to throw an exception.

### EXAMPLE 14-11

```cpp
// Using user-defined exception class divisionByZero with
// default error message.

#include <iostream>                                      //Line 1
#include "divisionByZero.h"                             //Line 2

using namespace std;                                     //Line 3

int main()                                               //Line 4
{
    int dividend, divisor, quotient;                    //Line 5
                                                         //Line 6
    try                                                //Line 7
    {
        cout << "Line 9: Enter the dividend: ";        //Line 8
        cin >> dividend;                                //Line 10
        cout << endl;                                   //Line 11

        cout << "Line 12: Enter the divisor: ";        //Line 12
        cin >> divisor;                                 //Line 13
        cout << endl;                                   //Line 14

        if (divisor == 0)                               //Line 15
            throw divisionByZero();                     //Line 16

        quotient = dividend / divisor;                  //Line 17
        cout << "Line 18: Quotient = " << quotient
             << endl;                                   //Line 18
    }                                                   //Line 19
    catch (divisionByZero divByZeroObj)                 //Line 20
    {                                                   //Line 21
        cout << "Line 22: In the divisionByZero "
             << "catch block: "
             << divByZeroObj.what() << endl;            //Line 22
    }                                                   //Line 23

    return 0;                                           //Line 24
}                                                       //Line 25
```

**Sample Run 1:** In this sample run, the user input is shaded.

```text
Line 9: Enter the dividend: 28
Line 12: Enter the divisor: 6
Line 18: Quotient = 4
```
