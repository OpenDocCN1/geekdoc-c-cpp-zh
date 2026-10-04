# 238 Repetition Statements

# Program 5.2

```
#include <iostream>
using namespace std;

int main()
{
    int i;

    while (i >= 1)
{
        cout << i << " *";
        i--; // subtract 1 from i
    }
    return 0;
}
```

The assignment statement in Program 5.2 initially sets the int variable i to to 10. The while statement then checks to whether the value of i is greater than or equal to 1. While the expression is true, the value of i is displayed by the cout statement, and the value of i is decremented by 1. When it finally reaches zero, the expression is false, and the program exits the while statement. Therefore, Program 5.2 produces the following display when it runs:

10 9 8 7 6 5 4 3 2 1

To illustrate the power of the while statement, consider the task of printing a table of numbers from 1 to 10 with the numbers' squares and cubes. You can do this with a simple while statement, as shown in Program 5.3.
When Program 5.3 runs, the following display is produced:

| NUMBER | SQUARE | CUBE |
|---|---|--|
| 1 | 1 | 1 |
| 2 | 4 | 8 |
| 3 | 9 | 27 |
| 4 | 16 | 64 |
| 5 | 25 | 125 |
| 6 | 36 | 216 |
| 7 | 49 | 343 |
| 8 | 64 | 512 |
| 9 | 81 | 729 |
| 10 | 100 | 1000 |