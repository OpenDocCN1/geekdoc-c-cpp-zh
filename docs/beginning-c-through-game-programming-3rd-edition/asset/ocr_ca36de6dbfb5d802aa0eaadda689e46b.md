# Figure 2.8

The number 5 is skipped with a continue statement, and the loop ends with a break statement.

![](bbox=[0.115, 0.105, 0.86, 0.395])

```
// Finicky Counter
// Demonstrates break and continue statements

#include <iostream>

using namespace std;

int main()
{
    int count = 0;
    while (true)
    {
        count += 1;

        //end loop if count is greater than 10
        if (count > 10)
        {
            break;
        }
    }
```