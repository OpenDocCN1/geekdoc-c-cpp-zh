16. (Program) Write, compile, and run a C++ program that asks the user to input two numbers. After your program accepts these numbers by using one or more cin object calls, have it check the numbers. If the first number entered is greater than the second number, the program should print the message "The first number is greater."; otherwise, it should print the message "The first number is not greater than the second." Test your program by entering the numbers 5 and 8 and then using the numbers 11 and 2. What will your program display if the two numbers entered are equal?

17. (Debug) The following program displays the message Hello there! regardless of the letter input. Determine where the error is and why the program always causes the message to be displayed.

```
#include <iostream>
using namespace std;
int main()
{
    char letter;

    cout << "Enter a letter: ";
    cin >> letter;
    if (letter = 'm')
        cout << "Hello there!" << endl;

    return 0;
}
```

# 4.3 Nested if Statements

As you have seen, an if-else statement can contain any valid C++ simple or compound statements, including another if-else statement. Therefore, one or more if-else statements can be included in either part of an if-else statement. Including one or more if statements inside an existing if statement is called a nested if statement. For example, substituting the one-way if statement

```
if (distance > 500)
    cout << "snap";
```

for statement1 in this if statement

```
if (hours < 9)
    statement1;
else
    cout << "pop";
```