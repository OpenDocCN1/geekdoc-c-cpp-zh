are different. Use the smallest possible `array` to solve this problem.

+   9. 7.14 (*Duplicate Elimination with `vector`*) Reimplement **Exercise 7.13** using a `vector`. Begin with an empty `vector` and use its `push_back` function to add each unique value to the `vector`.

+   10. 7.15 (*Two-Dimensional `array` Initialization*) Label the elements of a 3-by-5 two-dimensional `array` `sales` to indicate the order in which they’re set to zero by the following program segment:

```
```cpp
{
    for (size_t row{}; row < sales.size(); ++row) {
        for (size_t column{}; column < sales[row].size();
++column) {
            sales[row][column] = 0;
        }
    }
}
```
```

+   11. 7.16 (*Dice Rolling*) Write a program that simulates the rolling of two dice. The sum of the two values should then be calculated. [*Note:* Each die can show an integer value from 1 to 6, so the sum of the two values will vary from 2 to 12, with 7 being the most frequent sum and 2 and 12 being the least frequent sums.] **Figure 7.22** shows the 36 possible combinations of the two dice. Your program should roll the two dice 36,000,000 times. Use a one-dimensional `array` to tally