Do you want to enter another value (enter n to end)? n

The average of the 3 values you entered is 20.

After declaring and initializing the variables that you’re going to use, you start a for loop with no expressions specified, so there is no provision for ending it here. The block immediately following is the subject of the loop that is to be repeated.

The loop block performs three basic actions:

+   - It reads a value
+   - It adds the value read from cin to sum
+   - It checks whether you want to continue to enter values

The first action within the block is to prompt you for input and then read a value into the variable value. The value that you enter is added to sum and the count of the number of values, i, is incremented. After accumulating the value in sum, you are asked if you want to enter another value and prompted to enter 'n' if you have finished. The character that you enter is stored in the variable indicator for testing against 'n' or 'N' in the if statement. If neither is found, the loop continues; otherwise, a break is executed. The effect of break in a loop is similar to its effect in the context of the switch statement. In this instance, it exits the loop immediately by transferring control to the statement following the closing brace of the loop block.

Finally, you output the count of the number of values entered and their average, which is calculated by dividing sum by i. Of course, i is promoted to type double before the calculation, as you remember from the casting discussion in Chapter 2.

# Using the continue Statement

There is another statement, besides break, used to affect the operation of a loop: the continue statement. This is written simply as:

```
continue;
```

Executing continue within a loop starts the next loop iteration immediately, skipping over any statements remaining in the current iteration. I can demonstrate how this works with the following code.

```
#include <iostream>

using std::cin;
using std::cout;
using std::endl;

int main()
{
    int i = 0, value = 0, product = 1;
    for(i = 1; i <= 10; i++)
    {
        cout << "Enter an integer: ";
```