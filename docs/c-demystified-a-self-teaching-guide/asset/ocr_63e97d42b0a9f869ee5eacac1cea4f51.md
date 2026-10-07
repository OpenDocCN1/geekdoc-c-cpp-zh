return 0;

Without the break keyword, the for loop would be infinite due the lack of a second
expression. Again, however, I recommend against this use of the break keyword, and
point it out simply because other programmers believe differently—thus, you're likely to
encounter it at some point in time.

# # The Continue Keyword

You can also use the continue keyword in a for loop. The continue keyword, like the break
keyword, is used within the code of a for loop, commonly with an if/else structure. If the
continue statement is reached, the current iteration of the loop ends, and the next
iteration of the loop begins.

For example, in the following program, the user is charged $3 item, but not charged for
a "baker's dozen". In other words every 13th item is free—in other words, the user is charged for
ditems instead of 13.

```
#include <iostream>
using namespace std;
int main(void)
{
    int num, counter, total = 0;
    cout << "How many items you want to buy: ";
    cin >> num;
    for (int counter = 1; counter <= num; counter++) {
        if (counter % 13 == 0)
            continue;
        total += 3;
    }
    cout << "Total for " << num << " items is $" << total;
    return 0;
}
```

Here are three sample inputs and outputs, illustrating the change for the 12 or 13 items is
the, but on the 14th item the user is charged an additional $3. The reason
why the code charges the user no additional price for the 13th item is that the continue
statement is reached, preventing three dollars from being added to the total.

How many items you want to buy: 12
Total for 12 items is $36

How many items you want to buy: 13
Total for 13 items is $36

How many items you want to buy: 14
Total for 14 items is $39

While the continue keyword is part of the C++ language, I recommend, as I do with the
break keyword, that you use it sparingly. Normally, each iteration of a for loop has
end point. When you use a continue statement, each iteration has multiple end\points. This makes your code more difficult to understand, and can result in logic errors.

In the following program, the logical ! (Not) operator is another example of using the continue
keyword.