read will be added to zero (because `totalNumOfBoxesSold` is initialized to 0), giving the correct sum of the first number. To find the average, divide `totalNumOfBoxesSold` by `counter`. If `counter` is 0, then dividing by zero will terminate the program and you will get an error message. Therefore, before dividing `totalNumOfBoxesSold` by `counter`, you must check whether or not `counter` is 0.

Notice that in this program, the statement in Line 18 initializes the LCV counter to 0. The expression `counter < numOfVolunteers` in Line 19 evaluates whether `counter` is less than `numOfVolunteers`. The statement in Line 25 updates the value of `counter`.

# Case 2: Sentinel-Controlled `while` Loops

You do not always know how many pieces of data (or entries) need to be read, but you may know that the last entry is a special value, called a **sentinel**, that will tell the loop to stop. In this case, you must read the first item before the `while` statement so the test expression will have a valid value to test. If this item does not equal the sentinel, the body of the `while` statement executes. The `while` loop continues to execute as long as the program has not read the sentinel. Such a `while` loop is called a **sentinel-controlled while loop**. In this case, a `while` loop might look like the following:

```
cin >> variable;              //initialize the loop control variable

while (variable != sentinel)   //test the loop control variable
{
    .
    .
    cin >> variable;           //update the loop control variable
    .
    .
}
```

# EXAMPLE 5-4

The program in Example 5-3 computes and outputs the total number of boxes of cookies sold, the total money made, and the average number of boxes sold by each student. However, the program assumes that the programmer knows the exact number of volunteers. Now suppose that the programmer does not know the exact number of volunteers. Once again, assume that the data is in the following form: *student’s name* followed by a *space* and the *number of boxes sold by the student*. Because we do not know the exact number of volunteers, we assume that reading a value of −1 for name will mark the end of the data, since it is a highly unlikely name to run into. So consider the following program: