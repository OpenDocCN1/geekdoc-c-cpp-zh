# Operations

The stack interface creates an empty constructor. We can check the size and emptiness of a stack. The only member function that we can use to access the elements in the stack is the `top()` member function. The `push()` and `pop()` operations are used to insert into and erase an element from the stack, respectively.

# Application

The last-in-first-out nature of a stack makes it ideal for applications in which the first object we need to use in a collection of objects is the last one that we created.

In Chapter 10 we showed how to convert a decimal number to its equivalent hexadecimal number using a user-defined stack class. We repeat that example using the stack class defined in STL as shown in Program 19.11. Although the code is very similar to the one in

# Program 19.11  Coverting a decimal to hexadecimal

```
```cpp
/***************************************************************
 * Using a stack to change a decimal number to hexadecimal      *
 ***************************************************************/
#include <stack>
#include <iostream>
using namespace std;

int main()
{
    // Instantiation of a stack
    stack <char> stk;
    // Creation of two strings and a declaration of a variable
    string converter("0123456789ABCDEF");
    string hexadecimal;
    int decimal;
    // Inputting a decimal number
    do
    {
        cout << "Enter a positive integer: ";
        cin >> decimal;
    } while (decimal <= 0);
    // Creation of hexadecimal characters and push them into stack
    while (decimal != 0)
    {
        stk.push(converter[decimal % 16]);
        decimal = decimal / 16;
    }
    // Popping characters from stack and pushing into hex string
    while (!stk.empty())
    {
        hexadecimal.push_back(stk.top());
        stk.pop();
    }
    cout << "The hexadecimal number : " << hexadecimal;
    return 0;
}
```
```