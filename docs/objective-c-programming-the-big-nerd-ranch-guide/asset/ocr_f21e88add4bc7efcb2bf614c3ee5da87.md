```
#include <stdio.h>

int main (int argc, const char * argv[])
{
    // Declare the variable called 'weight' of type float
    float weight;

    // Put a number in that variable
    weight = 14.2;

    // Log it to the user
    printf("The turkey weighs %f.\n", weight);

    // Declare another variable of type float
    float cookingTime;

    // Calculate the cooking time and store it in the variable
    // In this case, '*' means 'multiplied by'
    cookingTime = 15.0 + 15.0 * weight;

    // Log that to the user
    printf("Cook it for %f minutes.\n", cookingTime);

    // End this function and indicate success
    return 0;
}

```

Build and run the program. You can either click the Run button at the top left of the Xcode window or use the keyboard shortcut Command-R. Then click the button to get to the log navigator. Select the item at the top labeled Debug Turkey to show your output. It should look like this:

```
The turkey weighs 14.200000.
Cook it for 228.000000 minutes.
```

Now click the button to return to the project navigator. Then select main.c so that you can see your code again. Let's review what you've done here.

In your line of code that looks like this:

```
float weight;
```

we say that you are “declaring the variable weight to be of type float.”

In the next line, your variable gets a value:

```
weight = 14.2;
```

You are copying data into that variable. We say that you are “assigning a value of 14.2 to that variable.”

In modern C, you can declare a variable and assign it an initial value in one line, like this:

```
float weight = 14.2;
```

Here is another assignment:

```
cookingTime = 15.0 + 15.0 * weight;
```

The stuff on the right-hand side of the = is an expression. An expression is something that gets evaluated and results in some value. Actually, every assignment has an expression on the right-hand side of the =.