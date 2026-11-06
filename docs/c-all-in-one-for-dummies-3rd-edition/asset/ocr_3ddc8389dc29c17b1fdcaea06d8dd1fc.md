Be careful when you are thinking through such `if` statements. You could have a situation where more than one condition can occur. For example, you may have something like the example shown in `IfElse3`:

```
```cpp
#include <iostream>

using namespace std;

int main()
{
    int i;

    cout << "Type any number: ";
    cin >> i;

    if (i > 100)
    {
        cout << "It's greater than 100." << endl;
    }
    else if (i > 10)
    {
        cout << "It's greater than 10" << endl;
    }
    else
    {
        cout <<
            "It's neither greater than 100 nor greater than 10."
            << endl;
    }

    return 0;
}
```
```

Think about what would happen if i is the number 150. The first condition, `i > 100`, is true. But so is the second condition, `i > 10`. The number 150 is greater than 100, and 150 is also greater than 10. So which block will the computer execute? Or will it execute both blocks?

The computer executes only the first condition that is satisfied. Thus, when i is 150, the computer prints the message "It's greater than 100." It does not print the other messages. In fact, the computer doesn’t even bother checking the other conditions at that point. It just continues with the application.

# Repeating Actions with Statements That Loop

Suppose that you’re writing an application to add all the numbers from 1 to 100. For example, you may want to know how much money you will get if you tell 100 people, “Give me one dollar more than the person to your left.” With a mastery of copy-and-paste, you could do something like this

```
```cpp
int x = 1;
x = x + 2;
x = x + 3;
x = x + 4;
```
```