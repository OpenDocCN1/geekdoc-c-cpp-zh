# 7.5 Copying an Array

Because arrays are reference types, you cannot create a separate copy of an array by assigning the reference variable to another reference variable. For example,
int[] temp1 = testScore;
will not create a copy of the array testScore. Instead, both temp and testScore will refer to the same array, as shown.

![](bbox=[0.04, 0.21, 0.89, 0.26])

That is, there is only one array, but two variables refer to it. That means if you change an element of testScore, in effect, you also are changing that element for temp1.

Step: 7-24: Add the following code to the end of the Click event handler of Demo button, and insert breaks at line 56 and 57:

```
53
54
55    // Assign testScore to another reference variable - doesn't copy the array
    int[] temp1 = testScore;
56    testScore[9] = 69;
57
```

Step 1-25: Run the project. When the program breaks at line 56 (before testScore[9] is changed to 69), expand testScore and temp in Locals window (Debug, Windows, Locals) and observe that temp has the same values as testScore.

Step 1-26: Click Run to continue execution. When the program breaks at line 57, expand testScore and temp in Locals window (Debug, Windows, Locals) and observe that temp[9] has same values as testScore[9], as shown in Figure 7-15, though it looks like you changed the value of only testScore.

# Figure 7-15: Changed value of temp1

![](bbox=[0.1, 0.68, 0.43, 0.85])

You may change any element of the array using temp1 or testScore. For example, temp1[8] would change the ninth element of the array that also is referenced by testScore.