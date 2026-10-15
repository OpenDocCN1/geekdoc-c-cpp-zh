```
// Fig. 5.1: fig05_01.cpp
// Counter-controlled repetition.
#include <iostream>
using std::cout;
using std::endl;

int main()
{
    int counter = 1; // declare and initialize control variable

    while ( counter <= 10 ) // loop-continuation condition
    {
        cout << counter << " ";
        counter++; // increment control variable by 1
    } // end while

    cout << endl; // output a newline
    return 0; // successful termination
} // end main
```

1 2 3 4 5 6 7 8 9 10

Fig. 5.1 | Counter-controlled repetition.

initialization are, in effect, executable statements. In C++, it is more precise to call a declaration that also reserves memory—as the preceding declaration does—a definition. Because definitions are declarations, too, we’ll use the term “declaration” except when the distinction is important.

The declaration and initialization of counter (line 9) also could have been accomplished with the statements

```
int counter; // declare control variable
counter = 1; // initialize control variable to 1
```

We use both methods of initializing variables.

Line 14 increments the loop counter by 1 each time the loop’s body is performed. The loop-continuation condition (line 11) in the while statement determines whether the value of the control variable is less than or equal to 10 (the final value for which the condition is true). Note that the body of this while executes even when the control variable is 10. The loop terminates when the control variable is greater than 10 (i.e., when counter becomes 11).

Figure 5.1 can be made more concise by initializing counter to 0 and by replacing the while statement with

```
while ( ++counter <= 10 ) // loop-continuation condition
    cout << counter << " ";
```

This code saves a statement, because the incrementing is done directly in the while condition before the condition is tested. Also, the code eliminates the braces around the body of the while, because the while now contains only one statement. Coding in such a con-