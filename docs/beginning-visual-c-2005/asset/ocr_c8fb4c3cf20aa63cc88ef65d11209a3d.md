blocks of data, such as arrays, that are defined outside the function. Most importantly, however, you will also see later that you can allocate space for variables dynamically, that is, during program execution. This sort of capability allows your program to adjust its use of memory depending on the input to the program. Because you don’t know in advance how many variables you are going to create dynamically, a primary way you have for doing this is by using pointers — so make sure you get the hang of this bit.

# Try It Out   Using Pointers

You can try out various aspects of pointer operations with an example:

```
//Ex4_05.cpp
// Exercising pointers
#include <iostream>
using std::cout;
using std::endl;
using std::hex;
using std::dec;

int main()
{
    long* pnumber = NULL;            // Pointer declaration & initialization
    long number1 = 55, number2 = 99;

    pnumber = &number1;              // Store address in pointer
    *pnumber += 11;                  // Increment number1 by 11
    cout << endl
         << "number1 = " << number1
         << "   &number1 = " << hex << pnumber;

    pnumber = &number2;              // Change pointer to address of number2
    number1 = *pnumber*10;           // 10 times number2

    cout << endl
         << "number1 = " << dec << number1
         << "   pnumber = " << hex << pnumber
         << "   *pnumber = " << dec << *pnumber;

    cout << endl;
    return 0;
}
```

On my computer, this example generates the following output:

```
number1 = 66     &number1 = 0012FEC8
number1 = 990    pnumber = 0012FEBC    *pnumber = 99
```

# How It Works

There is no input to this example. All operations are carried out with the initializing values for the variables. After storing the address of number1 in the pointer pnumber, the value of number1 is incremented indirectly through the pointer in this statement:

```
*pnumber += 11;            // Increment number1 by 11
```