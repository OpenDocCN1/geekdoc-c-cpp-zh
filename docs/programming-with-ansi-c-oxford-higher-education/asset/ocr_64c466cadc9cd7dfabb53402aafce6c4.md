# 8.12 terminate() AND unexpected() FUNCTIONS

As mentioned earlier, terminate() is the function that calls abort() to exit the program in the event of run-time error related to exceptions. The indirection through terminate() function is provided because the user can define his/her own terminate() function instead of the built-in terminate(), which just calls abort() and does nothing else. This way the user may be able to close all open files and deallocate resources before quitting the program. Let us see how this is done using the following program.

```
//SetTerminate.cpp
#include <exception>
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
void ExGen()
{
    cout << "Inside the function \n";
    cout << "Inside try block \n";
    cout << "Assuming error and throwing exception now \n";
    MyException Error1(20, "Error testing");
    throw Error1;
    cout << "This statement will not be executed";
}
void MyTerminate()
{
    cout << "This is my terminate function";
    /* The cleanup code comes here; it closes all open files,
    closes open connections, and runs destructors if need be */
    exit(-1);
```