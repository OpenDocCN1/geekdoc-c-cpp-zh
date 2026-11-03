```
// Fig. 4.2: fig04_02.c
// Counter-controlled iteration with the for statement.
#include <stdio.h>

int main(void)
{
    // initialization, iteration condition, and increment
    // are all included in the for statement header.
    for (unsigned int counter = 1; counter <= 10; ++counter) {
        printf("%u\n", counter);
    }
}
```

Fig. 4.2 | Counter-controlled iteration with the for statement.

# for Statement Header Components

Figure 4.3 takes a closer look at the for statement of Fig. 4.2. Notice that the for statement "does it all"—it specifies each of the items needed for counter-controlled iteration with a control variable. If there's more than one statement in the body of the for, braces are required to define the body of the loop—as we discussed in Section 3.6, you should always place a control statement's body in braces, even if it has only one statement.

![](bbox=[0.15, 0.62, 0.9, 0.78])

Fig. 4.3 | for statement header components.

# Control Variables Defined in a for Header Exist Only Until the Loop Terminates

When you define the control variable in the for header before the first semicolon (;), as in line 9 of Fig. 4.2:

```
for (unsigned int counter = 1; counter <= 10; ++counter) {
```

the control variable exists only until the loop terminates.

# Common Programming Error 4.2

> For a control variable defined in a for statement's header, attempting to access the control variable after the for statement's closing right brace (}) is a compilation error.

# Off-By-One Errors

Notice that Fig. 4.2 uses the loop-continuation condition counter <= 10. If you incorrectly wrote counter < 10, then the loop would be executed only 9 times. This is a common logic error called an off-by-one error.