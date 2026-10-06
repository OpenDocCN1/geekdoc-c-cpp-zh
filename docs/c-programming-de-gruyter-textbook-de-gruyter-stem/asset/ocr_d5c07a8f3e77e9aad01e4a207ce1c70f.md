# 54 2 Elementary C++ Programming

The execution order of a switch statement is: first calculate the value of the expression in a switch statement; then find the first case labeled by a constant expression that matches the value of the expression, use the case as an entry label, and start execution. If no case matches the value of the expression, then execute from "default":

You should pay attention to the following issues when using switch statements:

+   - The expression in switch statements are int-type, character-type, or enumeration-type.

+   - The value of each constant expression must be different, although their sequence order does not affect the execution result.

+   - There can be several statements in each case, and you do not need to use {}.
- Each case is only an entry label, and it cannot decide the endpoint of the execution. So you will need to add a break statement at the end of a case branch to exit early from the whole switch structure; otherwise execution will fall through to the next statement when the code of that case branch is done.
- When several branches need to do the same action, they can use the same group of statements.

**Example 2.4:** Enter an integer between 0–6, convert it into the corresponding day of week, and then output it.

Analysis: In this example, the number entered decides the output information, because numbers 0–6 represent seven conditions: "Sunday", "Monday".... Thus we need to use a multiple selection structure. Since it is judging the day of the week, a switch statement is most appropriate.

Source code:

```
//2_4.cpp
#include <iostream>
using namespace std;
int main()
{
    int day;

    cin >> day;
    switch (day)
    {
        case 0: cout << "Sunday" << endl;
            break;
        case 1: cout << "Monday" << endl;
            break;
        case 2: cout << "Tuesday" << endl;
            break;
        case 3: cout << "Wednesday" << endl;
            break;
    }
```