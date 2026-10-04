# Chapter 5 259

# Program 5.10

Did you figure it out? The loop starts with count initialized to 2, stops when count exceeds 20, and increments count in steps of 2. This is the output of Program 5.10:

+   2 4 6 8 10 12 14 16 18 20

As mentioned, the for statement doesnt require having an initializing or altering list inside parentheses; however, the two semicolons must be included in these parentheses. For example, the construction for ( ; count <= 20 ; ) is valid.
If the initializing list is missing, the initialization step is omitted when the for statement is executed. The programmer must provide the required initializations before the for statement is encountered. Similarly, if the altering list is missing, any expressions needing to alter the evaluation of the tested expression must be included in the statement part of the loop. The for statement only ensures that all expressions in the initializing list are executed once, before evaluation of the tested expression, and all expressions in the altering list are executed at the end of the loop, before the tested expression is rechecked. Program 5.10 can be rewritten in any of the three ways shown in Programs 5.10a, 5.10b, and 5.10c.

# Program 5.10a

```
#include <iostream>
using namespace std;
int main()
{
    int count;
    count = 2; // initializer outside the for statement
    for (; count <= 20; count = count + 2)
        cout << count << " ";
    return 0;
}
```