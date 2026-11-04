# Example 2.20. The for loop.

```
using System;

namespace Chapter2 {
    class Class1 {
        static void Main() {
            int iCounter_1;

            for (iCounter_1 = 0; iCounter_1 < 5; iCounter_1++) {
                Console.WriteLine(iCounter_1);
            }

            Console.WriteLine("Program complete!\n");
        }
    }
}
```

> **Program Walkthrough**
> 
> > The for statement begins by assigning our variable the value zero. This value is then compared to 5 and found true since zero is less than five. The incrementing operator then adds one to the value of our variable making its value one. The loop is then executed and our variable iCounter_1 is displayed. The loop then finds the variable is still less than five, and the variable is then incremented a second time. The third time the loop runs, our value increases to three, which is still less than five, so the loop runs again. The fourth iteration increases our value to four and the loop runs again. Finally, our value equals five and the loop terminates. The program moves to the next line "Program complete!" and the program ends.

Nesting is just as legal and useful in for loops as it is in the other loops introduced earlier, but it is also just as dangerous (or as trying) when you are caught in an infinite loop. Thus, you should avoid using the for loop's tracking variable for anything other than keeping track of that for loop. If you think you're up to it, you can go back and rewrite the while and do-while programs using only for loops.

The for loop can become an infinite loop or mindless hole with even the most subtle of errors. For example: