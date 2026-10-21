Inside the function
Inside try block
Press 1 for int, 2 for char, 3 for MyException, and 4 for string
1
Assuming error and throwing exception now
Integer exception10 is caught in the function
This will not be executed if the exception is not caught in the function
An integer is caught in main
Inside main
Inside the function
Inside try block
Press 1 for int 2 for char, 3 for MyException, and 4 for string
3
Assuming error and throwing exception now
Inside main catch
Error number is 20
Error testing

# 8.9 CATCH ALL

> catch (...) is used to catch any exception. Here, the three dots play the role of a wild card.

It is possible to catch all types of exceptions in a single catch section by using catch (...) (three dots as an argument).

Consider Program 8.4 which is reworked from the previous one. It has catch (...) (which is commonly known as the catch all statement) in the function. Now, whatever is thrown would be caught by that single statement and would not be passed up the hierarchy.

# PROGRAM 8.4 Catching all exceptions in a single catch

```
//CatchAll.cpp
#include <iostream>
#include <string>
using namespace std;
class MyException
{
private:
    int ExNumber;
    string ExMessage;
public:
    MyException(int ErrNo, string Description)
    {
        ExNumber = ErrNo;
        ExMessage = Description;
    }

    void ShowEx()
    {
        cout << "Error number is" << ExNumber << "\n";
        cout << ExMessage << "\n";
    }
};
```