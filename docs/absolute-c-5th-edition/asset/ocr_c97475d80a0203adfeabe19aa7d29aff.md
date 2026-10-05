# Loops 81

We described the break statement when we discussed the switch statement. The break statement consists of the keyword break followed by a semicolon. When executed, the break statement ends the nearest enclosing switch or loop statement. Display 2.8 contains an example of a break statement that ends a loop when inappropriate input is entered.

Display 2.8 A break Statement in a Loop

```
#include <iostream>
using namespace std;

int main ()
{
    int number = 0, count = 0;
    cout << "Enter 4 negative numbers:\n";

    while (++count <= 4) {
        cin >> number;
        if (number >= 0) {
            cout << "ERROR: positive number"
                 << " " or zero was entered as the next\n";
                 cout << "th number! Input ends "
                 << "with the " << count << "th number.\n";
                 count << "th number was not added in.\n";
            break;
        }
        sum = sum + number;
    }
    cout << sum << " is the sum of the first "
         << (count - 1) << " numbers.\n";

    return 0;
}
```

Sample Dialogue

![](bbox=[0.118, 0.824, 0.638, 0.946])