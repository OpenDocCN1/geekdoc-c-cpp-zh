![](bbox=[0.918, 0.076, 1.0, 0.243])

Also notice that when you break out of the loop, the application does not quit. It continues with the statements that follow the loop. In this case, it still prints the message **"All Finished!"**

![](bbox=[0.174, 0.165, 0.239, 0.233])

You can leave empty the second portion of the for statement (the condition) by simply putting a blank between the spaces. Then, to get out of the loop, you can use a break statement. However, doing that makes for messy code. You should treat messy code like you treat a messy house: Although sometimes everyone minds it, the truth is that most people don't care to see a messy house. And you really don’t want other people to see your messy house — or your messy code. Yes, as a programmer, being a little self-conscious is sometimes a good thing.

# ## Continuing

In addition to the times when you may need to break out of a loop for a special situation, you can also cause the loop to end its current iteration; but instead of breaking out of it, the loop resumes with the next iteration.

For example, you may be, again, reading data from over the Internet, and doing this by looping a specified number of times. In the middle of the loop, you may encounter some bad data. But rather than quit out of the loop, you may want to simply ignore the current piece of bad data and then continue reading more data.

To do this trick, you use a C++ statement called `continue`. The continue statement says, “End the current iteration, but continue running the loop with the next iteration.”

The ForLoop4 example that follows shows a slightly modified version of the previous example, in the “Breaking” section. When the loop gets to 5, it doesn’t execute the second cout line. But rather than break out of the loop, it continues with 6, and then 7, and so on until the loop finishes on its own:

```
```cpp
#include <iostream>

using namespace std;

int main()
{
    int i;
    for (i=0; i<10; i++)
    {
        cout << i << " ";
        if (i == 5)
```
```