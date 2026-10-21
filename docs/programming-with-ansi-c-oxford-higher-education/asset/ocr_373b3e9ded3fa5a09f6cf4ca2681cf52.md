unexpected circumstances. We have specified to use that function instead of the built-in unexpected() using the statement
set_unexpected(MyUnExpected);

As a result, the user-defined MyUnExpected() function is called.

# 8.13 uncaught_exception() FUNCTION

When an exception is thrown, it automatically invokes stack unwinding process. In this process, all the objects prior to the throw statement to the beginning of the try block are destroyed in the reverse order of their creation. It is possible that some of the objects that are being destroyed have destructors and that the destructor function might also throw an exception.

If at least one of the objects contains such a destructor, we have a situation where the first exception is not completely handled, and the second one is being thrown. It is not possible in C++ to handle two exceptions simultaneously. The normal outcome of such a situation is a call to abort(), which terminates the program. In such situations, a function from built-in exception class, uncaught_exception(), comes handy. It returns true when an exception is thrown. If the destructor checks and finds that an exception has already been thrown when the destructor is called, it will not throw a new one. The algorithm of the function would be as follows:

```
if(uncaught_exception())
{
    Do not call the function that might throw an exception
}
else
{
    Follow the natural sequence of the destructor algorithm
}
```

Uncaught_exception is a handy way of finding out unhandled exceptions.

Program 8.5 demonstrates the use of the uncaught_exception() function. When an exception is thrown, the destructors of all the objects defined in the try block are called one by one. Then, the exception is handled and now it is said to be caught. If we check for the uncaught exception now, it is found to be caught.

# PROGRAM 8.5 Using uncaught_exception to find out unhandled exceptions

```
//UncaughtException.cpp
#include <exception>
#include <iostream>
using namespace std;

class TestClass
{
    char *ptrMessage;
public:
    TestClass(char Message[], int LengthOfMessage)
    {
        ptrMessage = new char [LengthOfMessage + 1];
        for(int i = 0; i < LengthOfMessage; i++)
        {
            ptrMessage[i] = Message[i];
        }
        ptrMessage[LengthOfMessage] = 0; // Null
```