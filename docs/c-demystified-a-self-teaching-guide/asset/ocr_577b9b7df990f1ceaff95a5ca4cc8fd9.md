```
#include <iostream>
using namespace std;
int main(void) {
    int num, counter, total = 0;
    cout << "How many items do you want to buy: ";
    cin >> num;
    bool keeping = true;
    for (int counter = 1; counter <= num; counter++) {
        if (!counter % 13 == 0)) {
            total += 3;
        }
    }
    cout << "Total for " << num << " items is $$\ << total;
    return 0;
}
```

Note You could also use the relational != (not equal) operator, changing the statement to if (counter % 13 != 0 ).

# Nesting Loops

You can nest a for loop just as you can nest statements. For example, the following program prints five rows of ten X characters:

```
#include <iostream>
using namespace std;
int main(void) {
    for (int x = 1; x <= 5; x++) {
        for (int y = 1; y <= 10; y++) {
            cout << "X";
        }
        cout << "\n";
    }
    return 0;
}
```

The for loop for (int x = 1; x <= 5; x++) is the outer loop. The for loop for (int y = 1; y <= 10; y++) is the inner loop.

With nested loops, for each iteration of the outer loop, the inner loop goes through all its iterations. By analogy, a clock, minutes the outer loop, seconds the inner loop. In an hour, there are 60 iterations of minutes, but for each iteration of a minute, there are 60 iterations of seconds.

In the rows and columns, the first iteration of the outer loop, the inner loop goes through all ten of its iterations, printing X characters and one new line character. Then, for the next iteration of the outer loop, the inner loop again again through all of its iterations, printing X characters and one new line character. The same thing happens on the third, fourth, and fifth iterations of the outer loop, resulting in five rows of ten X characters.

While nested loops can be used to print rows and columns for tables, they also have uses. For example, the following program prompts for the total number of salespeople as well as the number of salespersons the user input