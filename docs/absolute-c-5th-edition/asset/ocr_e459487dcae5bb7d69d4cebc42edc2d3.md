# Loops

sets the value of result equal to 4. However, the value that the following gives to result is unpredictable, because it does not guarantee that the expressions are evaluated in order:

result = (first = 2, second = first + 1, third = second + 1);

For example, third = second + 1 might be evaluated before second = first + 1.1

# 2.6 The Increment Operator in an Expression

```
#include <iostream>
using namespace std;

int main() {
    int numberOfItems, count,
    caloriesForItem, totalCalories;

    cout << "How many items did you eat today?";
    cin >> numberOfItems;
    totalCalories = 0;
    count = 1;
    cout << "Enter the number of calories in each of the\n"
         << numberOfItems << " items eaten:\\";

    while (count++ <= numberOfItems) {
        cin >> caloriesForItem;
        totalCalories = totalCalories + caloriesForItem;
    }

    cout << "Total calories eaten today = "
         << totalCalories << endl;
    return 0;
}
```

Sample Dialogue

| How many items did you eat today? 7 |
 Enter the number of calories in each of the 7 items eaten:
 300 60 1200 600 150 1 120 |
 Total calories eaten today = 2431 |

> The C++ standard does specify that the expressions joined by commas should be evaluated left to right. However, our experience has been that not all compilers conform to the standard in this regard.