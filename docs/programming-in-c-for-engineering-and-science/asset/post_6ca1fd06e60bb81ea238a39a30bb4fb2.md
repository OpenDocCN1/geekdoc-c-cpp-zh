
and then reads the user's response from the keyboard. If it is y or Y, another data value is read. This continues until the user answers something other than y or Y, and the loop condition

```
response == 'y' || response == 'Y'
```

then terminates the repetition.

## Example 9.10 The Query Approach

```
/* This program uses a query-controlled loop to process a collection of failure times and find the mean time to failure.

    Input:  a collection of component failure times and user's
            response to "more data?" query
    Output: prompts and the average of the failure times
--------------------------------------------------------------------------*/

#include <iostream>          // <<, >>, cout, cin
using namespace std;

int main()
{
    cout << "Computing Component Mean Time to Failure\n\n";

    int numComponents;
    double failureTime,
           failureTimeSum = 0.0;

    char response;
    do
    {
        cout << "\nEnter a failure time: ";
        cin >> failureTime;

        failureTimeSum += failureTime;
        numComponents++;

        cout << "Do you have more data to enter (y or n)? ";
        cin >> response;
    }
    while (response == 'y' || response == 'Y');

    cout << "\nThe mean failure time of the "
         << numComponents << " components is "
         << failureTimeSum / numComponents << endl;
}
```

# SAMPLE RUN:

Computing Component Mean Time to Failure

Enter a failure time: 2.3
Do you have more data to enter (y or n)? y

Enter a failure time: 2.4
Do you have more data to enter (y or n)? y

Enter a failure time: 2.5
Do you have more data to enter (y or n)? y

Enter a failure time: 2.6
Do you have more data to enter (y or n)? y

Enter a failure time: 2.1
Do you have more data to enter (y or n)? n

The mean failure time of the 5 components is 2.38

In problems where it is reasonable to assume that there is at least one data value to be entered and processed, the query and the corresponding loop condition are placed at the bottom of the loop, making it a posttest loop.⁵ This suggests the following pattern for a query-controlled input loop:

# PATTERN FOR QUERY-CONTROLLED INPUT LOOP

```
char response;
do
{
    Display a prompt for a data value.
    Read the Value to be processed.
    Process the Value.
    Display a query that asks if there is more data.
    Input the user's response (y or n)
}
while ((response != 'n' && (response != 'N')));
```

⁵ To allow no values to be entered and processed, a forever loop can be used:

```
for (;;)
{
    cout << "\nDo you wish to continue (y or n)? ";
    char response;
    cin >> response;
    if (response == 'n' || response == 'N') break;
    cout << "\nEnter a value: ";
    double value;
    cin >> value;
    // process value
}
```

### 9.5.4.1 Query Functions

The code to perform a query tends to clutter a loop, which may obscure the program’s structure, especially if the query is lengthy, perhaps due to special instructions to the user. One way to avoid this is to use a query function like the following to perform the query, read the user’s response, and return true or false based on the response, thus hiding the actual code that does the querying:

```
bool moreData()
{
    char answer;
    cout << "Do you have more values to enter (y or n)? ";
    cin >> answer;
    return (answer == 'y') || (answer == 'Y');
}
```

Because it returns a boolean value, a call to such a query function can be used as a loop condition. For example, we could modify the mean-time-to-failure program of Example 9.10 to use the query function moreData() to control the input loop:

```
int main()
{
    .
    .
    .
    do
    {
        cout << "\nEnter a failure time: ";
        cin >> failureTime;
        failureTimeSum += failureTime;
        numComponents++;
    }
    while ( moreData() );
    .
    .
    .
}
```

Each time execution reaches the loop condition, the function moreData() is called. It queries the user, reads the response, and returns true if the response was either y or Y and returns false otherwise. If moreData() returns true, the body of the do loop is repeated, but if it returns false, repetition is terminated.

```
initialization statements
Loop
    statement₁
    .
    .
    .
    statementₙ
End loop
```

Finally, formulate an appropriate termination condition. Then, determining where it should be placed in the loop will lead to which kind of loop to use:

If the termination condition appears

- at the beginning of the loop, it’s a pretest loop; choose a while loop;
- at the bottom of the loop, it’s a posttest loop; choose a do loop;
- within the list of statements, it’s a test-in-the-middle loop; choose a forever loop with an if-break (or if-return) combination.

To demonstrate this procedure, let’s look again at the bouncing-ball problem in Section 9.3. Using a generic loop, we might use the following as a first version of the algorithm:

- 1. Initialize bounce to 0.
- 2. Enter a value for height and display it.
- 3. Loop
  a. Replace height with height divided by 2.
  b. Increment bounce by 1.
  c. Display bounce and height.
  End loop

As a termination condition for the loop, we can use

```
height < SMALL_NUMBER
```

because repetition is to stop when height is less than some SMALL_NUMBER. However, the user could have entered zero or a negative value for height, in which case the body of the loop should not be executed. Thus, we should evaluate this condition immediately upon entering the loop:

- 1. Initialize bounce to 0.
- 2. Enter a value for height.

# CHAPTER SUMMARY

# Key Terms

analysis of algorithms
break statement
continue statement
counting (or counter-controlled) loops
do loop
do statement
end-of-data flag
end-of-file mark
for loop
forever loop
grows linearly
if-break combination
indefinite loop

initialization list
nested loops
one-trip behavior
posttest loop
pretest loop
query-controlled loop
query function
sentinel
test-at-the-bottom loop
termination condition
trace table
while loop
zero-trip behavior

# NOTES

- A trace table is a useful tool (especially in debugging) to trace the action of a loop.
- A for statement can be used to step through a range of values with any increment by using an appropriate increment expression.
- An indefinite loop can be implemented in C++ with a for statement with no loop condition—for(;;){ ... }—or a while statement of the form while(true){ ... } can be used.
- A forever loop continues repetition when its termination condition is false and terminates repetition when that condition is true.
- A break statement can be used to terminate execution of an enclosing loop. It terminates the innermost enclosing loop.
- In some cases, a return statement is a useful alternative to break for terminating execution of a function and returning to the calling function.
- A continue statement is useful for skipping the rest of the current iteration and beginning a new one.

- A *while* loop is a pretest (or test-at-the-top) loop. It continues repetition so long as its condition is true, and terminates repetition when that condition is false. A while loop has *zero-trip* behavior.

- A *do* loop is a posttest (or test-at-the-bottom) loop. Because its loop body will always be executed at least once before the loop condition is tested, it is said to have *one-trip* behavior.

- Three common kinds of input loops are:

- *counting* loops in which the number of input items is known in advance;

- *sentinel-controlled* loops in which an end-of-data flag (or sentinel) signals the end of data;

- *query-controlled* loops in which the user is asked whether there is more data.

- The following guidelines may help with deciding which kind of loop to use:

1. If the algorithm requires counting through some fixed range of values, use a counting loop.

2. If a general loop is required, use a generic indefinite loop to formulate the algorithm. Then determine where the termination condition should go. If at the beginning, use a while loop; if at the end, use a do loop; if somewhere else, use a forever loop with an if-break or if-return.

# Style and Design Tips

In this text, we use the following conventions for formatting the repetition statements considered in this chapter.

- The statement in a for, while, do, and forever loop is indented. If the statement is compound, the curly braces are aligned with the for, while, or do, and the statements inside the block are indented. In a do loop, do is aligned with its corresponding while.

```
for (...)
    statement

while(loop_condition)
    statement
```

```
for (...)
{
    statement₁
    ...
    statementₙ
}

while(loop_condition)
{
    statement₁
    ...
    statementₙ
}
```
