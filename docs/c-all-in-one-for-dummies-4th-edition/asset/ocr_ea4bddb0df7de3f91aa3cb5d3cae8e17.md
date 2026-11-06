partitions in which you can place a single value in each partition. Book 5, Chapter 1 tells you more about working with arrays.

![](bbox=[0.163, 0.148, 0.228, 0.215])

The for loop condition looks really strange. The condition looks like this: `int i : range`. The code creates an `int` value `i` that receives one value from the range for each iteration of the loop. The range (`:`) operator appears between the range declaration (`i`) and the range expression (`range`). This is a somewhat new feature of C++, and you’ll find it extremely useful for processing storage containers like arrays.

After `i` receives a value, the code outputs it to the screen using `cout`. What you see as output is the values 1 through 5 — each on a separate line. Of course, you might think this is all smoke and mirrors. So, try changing one of the values in the array and you see that the output changes to match the array content.

# Placing a condition within the declaration

Sometimes you need to perform data manipulation within a for loop in a way that’s more convenient than trying to manipulate it in a code block. You can actually create a special kind of condition within a for loop declaration in which the condition does something like access a part of a string or array. The ForLoopCondition example demonstrates how to perform this task, as shown here:

```
```cpp
#include <iostream>

using namespace std;

int main()
{
    string hello = "Hello";
    for (int i = 0; char c = hello[i]; i++)
    {
        cout << c << endl;
    }
    return 0;
}
```
```

Notice that the middle condition, which normally checks for a particular value or performs some other logical function, actually creates a new char variable, c, and places a letter from the `hello` string into it based on the value of `i`. After scratching your head for a while looking for the means of ending the loop, you determine that when the loop gets to the end of the string, it automatically ends.