# Figure 7-18: temp2 created by copying testScore

testScore

![](bbox=[0.04, 0.12, 0.75, 0.16])

temp2

![](bbox=[0.04, 0.2, 0.75, 0.24])

For example, executing the statement

```
testScore[9] = 99
```

changes the last element of testScore, but it does not affect temp2 or temp3.

However, temp1 is changed because temp1 was assigned the reference to testScore using the following statement; thus, both temp1 and testScore point to the same array:

```
int[] temp1 = testScore;
```

# Step 1-29: Add the following code to change the last element of testScore to 99.

```
testScore[9] = 99;
```

# Step 1-30: Run the project. When the program breaks at line 66, display Locals window and observe that the last element of testScore and temp1 is 99, but the last element of temp2 and temp3 is unchanged.

# Copying an Array Using a for Loop

You also may use a for loop to copy the elements of an array to another array. Here is the code that copies the elements of testScore to an array named temp4:

```
int[] temp4 = new int[10]; // or, int[] temp4 = new int[testScore.Length]
for (int index = 0; index <= testScore.Length - 1; index = index + 1)
    temp4[index] = testScore[index];
```

Here, the index is varied from 0 to the upper limit to access each element. So, the statement within the loop is equivalent to 10 different statements:

```
temp4[0] = testScore[0];
temp4[1] = testScore[1];
temp4[2] = testScore[2];
etc.
```