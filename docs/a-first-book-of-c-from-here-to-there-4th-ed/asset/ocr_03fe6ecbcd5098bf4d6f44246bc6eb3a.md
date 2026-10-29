```
for (num = 1; num <= MAXNUMS; num++)
    cout << setw(3) << num << " "
         << setw(3) << num * num << " "
         << setw(4) << num * num * num << endl;

return 0;
}
```

When Program 5.10 is run, this is the display produced:

| NUMBER | SQUARE | CUBE |
|---:|---:|---:|
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

Simply changing the number 10 in the for statement of Program 5.10 to 1000 creates a loop that’s executed 1000 times and produces a table of numbers from 1 to 100. As with the while statement, this small change produces an immense increase in the program’s processing and output. Notice also that the expression num++ was used in the altering list in place of the equivalent num = num + 1.

# Interactive for Loops

Using the cin object inside a for loop creates an interactive for loop, much like using this object in a while loop. For example, in Program 5.11, a cin object is used to input a set of numbers. As each number is input, it’s added to a total. When the for loop is exited, the average is calculated and displayed.

# Program 5.11

```
#include <iostream>
using namespace std;

// This program calculates the average
// of MAXCOUNT user-entered numbers
int main()
{

```