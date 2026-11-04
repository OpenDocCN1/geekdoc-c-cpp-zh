sections include descriptions of prototypes, global and local variables, data structures, and *return* statements all of which are crucial to that definition, so try to be patient.

A second way to write a simple do-nothing function is to place it under the main function as in Example 2.33. If you take a moment to examine this example, you'll find that it is relatively unchanged in regard to its contents and purpose (this being to do nothing). The minor revision simply moves the completed function out of the way while we return to work on the main method.

# Example 2.33. Our second function call.

```
using System;

namespace Chapter2 {
    class Class1 {
        static void Main() {
            OurFunction();
        }

        static void OurFunction() {
            /* This is a do nothing function */
        }
    }
}
```

# Variable Scope

*Local variables* are variables declared inside the main or subsequent methods. Their values are not known beyond the limitations of their block. Programmers who wish to transfer data from one block to another must do so using a referencing function. There are generally two types of passing variables: *calls-by-mechanism*, where information is merely passed to new variables, and *calls-by-reference*, which allow the programmer to alter the original memory locations. Local variables, as well as their secondary counterparts, can be passed and repassed endlessly, so limitations are minimized. In addition, user-defined functions have the ability to return data to the main or other calling functions.

C# doesn't actually allow for truly global variables, but the word global can be used to distinguish between localized and inclusive variables within a single method or class. *Global variables* allow for the exchange of data, but do not require a passing variable (see Example 2.34).