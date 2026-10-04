# 408 Arrays

```
double stdDev(int nums[], int numel, double av)
{
    int i;
    double sumdevs = 0.0;
    for (i = 0; i < numel; i++)
        sumdevs = sumdevs + pow(nums[i] - av),2);
    return(sqrt(sumdevs/numel));
}
```

A test run of Program 7.10 produced the following display:
The average of the numbers is 76.40
The standard deviation of the numbers is 13.15

Although this result agrees with the previous hand calculation, testing isn't complete without verifying the calculation at the boundary points. For this program, the test consists of checking the calculation with all the same values, as all 0s and all 100s. Another simple test is to use five 0s and five 100s. You can try these tests on your own as an exercise.

![](bbox=[0.105, 0.495, 0.175, 0.555])

# EXERCISES 7.5

+   1. (Practice) Enter and run Program 7.10 on your computer.
2. (Practice) Run Program 7.10 to determine the average and standard deviation of the following list of 15 grades: 68, 72, 78, 69, 85, 95, 75, 77, 82, 84, 91, 89, and 74.
3. (List Maintenance) A common problem is maintaining a list in numerical or alphabetical order. For example, inventory part numbers are typically kept in numerical order, but telephone lists are kept in alphabetical order.
For this exercise, write a function that inserts a three-digit part into a list of part numbers. The list is maintained in increasing numerical order, and duplicate part numbers aren't allowed. Allocate a maximum list size of 100 values, and use a sentinel value of 9999 to indicate the end of the list. For example, if the current list contains nine part numbers, the 10th position in the list contains the sentinel value. Figure 7.12 shows