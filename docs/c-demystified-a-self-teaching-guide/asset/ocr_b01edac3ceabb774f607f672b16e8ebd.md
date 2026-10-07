tenth iteration of the loop, which executes in the following order:

+   1. The current value of num, 10, is compared to 10.

+   2. Since the comparison is true (10 is less than or equal to 10), the current value of num, 10, is outputted.

+   3. The value of num is incremented, the current value of num, 11, is compared to 10. Since the

comparison is false (11 is not less than or equal to 10), the loop ends. The code inside
for loop does not execute, the value of num is not incremented, and the code
following the for executes. In this example, the code following the for loop is
return 0 statement, so the program ends.

The preceding examples used the increment operator. However, you can also
use the decrement operator. Changing the parentheses the keyword to
(int num = 10; num >= 1; num--) would result in the numbers between 1 and 10
being outputted in reverse: Note that the relational operator is changed from >==

In example of the output between 1 and 10, only one statement
belonged to the loop. However, as with the structure, if more than one statement
belong to the for, the statements must be contained within curly braces.

```
for (int num = 1; num < 10; num++) {
    cout << num << " ";
    cout << "Next loop ";
}
```

Also, as with the structure, the statement or statements will not execute for the keyword and
parenheses will not execute if the parentheses are followed by a semi-colon that
would be interpreted as an empty statement. Accordingly, in the following code fragment,
only the number that would output is:

```
for (int num = 1; num <= 10; num++)
    cout << num << " ";
```

The reason out would be 11 if the loop continues, and the empty statement
executes, until the condition fails when num is 11. The statement is not part of the
loop, it executes when the for loop completes, outputting 11, the value of num after the
loop finishes.

The expressions do not need to be inside the parentheses for the loop. In the
program, num is initialized before the loop, and is incremented inside the
body of the loop.

```
#include <iostream>
using namespace std;
int main(void) {
    int num = 1;
    for (; num <= 10;) {
        cout << num << " ";
        num++;
    }
    return 0;
}
```