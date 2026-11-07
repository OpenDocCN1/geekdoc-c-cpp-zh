![](bbox=[0.25, 0.08, 0.75, 0.22])

der is the value of the current hexadecimal digit, and the quotient is used to create the next digit. The process is repeated until the quotient is zero. However, the hexadecimal digits created are in the reverse order. We can push them into a stack and then pop them from the stack to put them in order, as shown in Figure 18.13.

Program 18.7 is a simple program for changing a decimal number to a hexadecimal number. To print the hexadecimal number, we must insert it in a string because the characters A to F are not digits in C++. We also use a string object named converter that holds the characters that can be found in a hexadecimal number. This string avoids a *switch* statement with 16 cases. We use the value created as the remainder as the index to the converter string.

# Program 18.7 Converting from decimal to hexadecimal

```
```cpp
/*****************************************************
 * The application program to change a decimal number to its *
 * hexadecimal equivalent                                       *
 *****************************************************/

#include "stack.cpp"

int main ( )
{
    // Instantiation of a Stack object
    Stack<char> stack;
    // Instantiation of two string objects and two integer variables
    string converter ("0123456789ABCDEF");
    string hexadecimal;
    int decimal;
    int index;
    // Input the decimal number
    do
    {
        cout << "Enter a positive integer: ";
        cin >> decimal;
    } while (decimal <= 0);
    cout << "The decimal number: " << decimal << endl;
```
```