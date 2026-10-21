program. At each point in your code where the debugger stops, you can inspect or even change the values of variables before continuing. You can also change the source code, recompile and then restart the program from the beginning. You can even change the source code in the middle of stepping through a program. When you move to the next step after modifying the code, the debugger automatically recompiles before executing the next statement.

To understand the basic debug capabilities of Visual C++ 2005, you will use the debugger on a program that you are reasonably sure works. You can then just pull the levers to see how things operate. Take a simple example from back in Chapter 4 that uses pointers:

```
```cpp
// Ex4_05.cpp
// Exercising pointers
#include <iostream>
using namespace std;

int main()
{
    long* pnumber = NULL;                 // Pointer declaration & initialization
    long number1 = 55, number2 = 99;

    pnumber = &number1;                   // Store address in pointer
    *pnumber += 11;                       // Increment number1 by 11
    cout << endl
         << "number1 = " << number1
         << "    &number1 = " << hex << pnumber;

    pnumber = &number2;                   // Change pointer to address of number2
    number1 = *pnumber*10;                 // 10 times number2

    cout << endl
         << "number1 = " << dec << number1
         << "    pnumber = " << hex << pnumber
         << "    *pnumber = " << dec << *pnumber;

    cout << endl;
    return 0;
}
```
```

If you still have this example on your system, just open the project; otherwise, you need to enter it again.

When you write a program that doesn’t behave as it should, the debugger enables you to inspect work through a program one step at a time to find out where and how it’s going wrong, and to inspect the state of your program’s data at any time during execution. You arrange to execute this example one statement at a time and to monitor the contents of the variables that you are interested in. In this case you want to look at pnumber, the contents of the location pointed to by pnumber (which is *pnumber), number1, and number2.

First you need to be sure that the build configuration for the example is set to Win32 Debug rather than Win32 Release (this is the default, unless you’ve changed it). The build configuration selects the set of project settings for the build operation on your program that you can see when you select the Project/Settings menu option. The current build configuration in effect is shown in the pair of adjacent drop-down lists on the Standard toolbar. To display or remove a particular toolbar you just right-click the