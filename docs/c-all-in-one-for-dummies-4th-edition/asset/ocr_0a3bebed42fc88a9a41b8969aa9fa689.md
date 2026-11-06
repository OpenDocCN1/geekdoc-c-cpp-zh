# Breaking

Suppose that you are writing an application that reads data over the Internet, and the loop runs for the amount of data that’s supposed to come. But midway through the process, you may encounter some data that has an error in it, and you may want to get out of the for loop immediately.

C++ includes a handy little statement that can rescue you in such a situation. The statement is called break. Now, nothing actually breaks, and it seems a bit fright­ening to write an application that instructs the computer to break. But this use of the term break is more in line with “break out of prison” than “break the computer.” But instead of breaking out of prison, it breaks you out of the loop.

The ForLoop3 example that follows demonstrates this technique. This sample checks for the special case of i equaling 5. You could accomplish the same result by changing the end condition of the for loop, but at least it shows you how the break statement works.

```
```cpp
#include <iostream>

using namespace std;

int main()
{
    for (int i=0; i<10; i++)
    {
        cout << i << " ";
        if (i == 5)
        {
            break;
        }
        cout << i * 2 << endl;
    }
    cout << "All Finished!" << endl;
    return 0;
}
```
```

In the preceding code, the first line inside the for loop, cout << i << " ";, runs when i is 5. But the final line in the for loop, cout << i * 2 << endl;, does not run when i is 5 because you tell it to break out of the loop between the two cout statements.