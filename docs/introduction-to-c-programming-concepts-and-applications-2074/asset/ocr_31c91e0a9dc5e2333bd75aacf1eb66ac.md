All that the for statement has to do is the condition; unlike the while loop, it's possible to omit the initialization and the update from inside the for statement.

For example, in this version of the code, you keep the initialization outside the for statement. You still need the semicolon to separate the different parts, but you can just leave out the first part.

Normally, the advantage of the for loop is that all the information needed to understand the loop will be contained inside the for statement—the parentheses. It makes it easier to understand how the loop works if the initialization, condition, and update are all in one place.

After that third iteration, the variable has the value 4, so it's no longer than 4, and thus the loop won't go through another iteration. After the loop, the value of i is 4, so you output the final line loop: 4.

The point is that the variable you have controlling the loop—known as the loop control variable—still has a value afterward. Typically, it will be the first value that caused the condition to fail.

And in this version, you also omit the update part, putting the update back into the loop explicitly. So, the for statement, in instance is working exactly like the while statement, except the condition is surrounded by semicolons on both sides.

Just like we can use conditional statements, we can nest loops. This is useful when you want to

```
10 int numpays = 0;
11 for (int numpays < 5; numpays++) {
```

```
// Program 5_16
// Illustrating value of variable after a loop
#include <iostream>
using namespace std;
int main() {
    int i;
    for (i = 1; i < 4; i++) {
        cout << "In loop: " << i << endl;
    }
    cout << "After loop: " << i << endl;
}
```

```
10 int numpays = 0;
11 for (int numpays < 5); {
12 cout << "Balance after " << numpays
13 << " payments is: " << balance << * interest << endl;
14 balance += interest;
15 balance -= payment;
16 numpays++;
17 }
```

In this very simple loop, notice that the for statement has a variable i that starts at 1 and continues less than 4, incrementing by i each time. The loop will output loop: 1, In loop: 2, and In loop: 3.

But there's not much point in using a for statement like this; you might well use a while statement.