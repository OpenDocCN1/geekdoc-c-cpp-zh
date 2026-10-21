Within the function, the value received from the calling program is displayed onscreen. Although the statement is essentially the same as the one used to output the address stored in a pointer, because num is now a reference, you obtain the data value rather than the address.

> This clearly demonstrates the difference between a reference and a pointer. A reference is an alias for another variable, and therefore can be used as an alternative way of referring to it. It is equivalent to using the original variable name.

The output shows that the function incr10() is directly modifying the variable passed as a caller argument.

You will find that if you try to use a numeric value, such as 20, as an argument to incr10(), the compiler outputs an error message. This is because the compiler recognizes that a reference parameter can be modified within a function, and the last thing you want is to have your constants changing value now and again. This would introduce a kind of excitement into your programs that you could probably do without.

This security is all very well, but if the function didn’t modify the value, you wouldn’t want the compiler to create all these error messages every time you pass a reference argument that was a constant. Surely there ought to be some way to accommodate this? As Ollie would have said, ‘There most certainly is, Stanley!’

# Use of the const Modifier

You can apply the const modifier to a parameter to a function to tell the compiler that you don’t intend to modify it in any way. This causes the compiler to check that your code indeed does not modify the argument, and there are no error messages when you use a constant argument.

# Try It Out Passing a const

You can modify the previous program to show how the const modifier changes the situation.

```
// Ex5_08.cpp
// Using a reference to modify caller arguments

#include <iostream>
using std::cout;
using std::endl;

int incr10(const int& num);    // Function prototype

int main(void)
{
    const int num = 3;    // Declared const to test for temporary creation
    int value = 6;

    cout << endl
         << "incr10(num) = " << incr10(num);

    cout << endl
```