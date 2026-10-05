+   - Statements of a case should always end with break.
Exceptions to this rule are very rare and should be clearly highlighted with a comment. If you forget this break, the statements of the next case will be executed, regardless of what its constant is. This is called fall-through.

![](bbox=[0.264, 0.273, 0.735, 0.477])

**Figure 8.6** Flowchart of a "switch" statement.

In Figure 8.6, you can see the flowchart of the switch construct. Although the break statements do not strictly belong to the switch flowchart, I have included them here as an option because they are so common and important.

The very simple calculator from Listing 8.18 places digits in a stack. An arithmetic operation takes the top elements of the stack and places the result back on top.

```
// https://godbolt.org/z/Y4W1loW8b
#include <string>
#include <vector>
#include <iostream>                                // cout

void calculator(std::ostream& out, std::string input) {
```