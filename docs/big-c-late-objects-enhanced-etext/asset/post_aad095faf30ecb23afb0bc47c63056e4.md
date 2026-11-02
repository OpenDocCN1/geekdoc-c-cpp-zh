
![](img/d61019b035dd82beb581604273c0ee6b_180_0.png)

## Figure 3 Execution of a for Loop

- The initialization is executed once, before the loop is entered. ①
- The condition is checked before each iteration. ② ⑤
- The update is executed after each iteration. ④

A for loop can count down instead of up:

```
for (counter = 10; counter >= 0; counter--) . . .
```

The increment or decrement need not be in steps of 1:

```
for (counter = 0; counter <= 10; counter = counter + 2) . . .
```

So far, we assumed that the counter variable had already been defined before the for loop. Alternatively, you can define a variable in the loop initialization. Such a variable is defined only in the loop:

```
for (int counter = 1; counter <= 10; counter++)
{
}
// counter no longer defined here
```

See Table 2 for additional variations.

## Programming Tip 4.2
### Choose Loop Bounds That Match Your Task

Suppose you want to print line numbers that go from 1 to 10. Of course, you will want to use a loop

```
for (int i = 1; i <= 10; i++)
```

The values for i are bounded by the relation 1 ≤ i ≤ 10. Because there are ≤ on both bounds, the bounds are called symmetric.

When traversing the characters in a string, it is more natural to use the bounds

```
for (int i = 0; i < str.length(); i++)
```

In this loop, i traverses all valid positions in the string. You can access the ith character as str.substr(i, 1). The values for i are bounded by 0 ≤ i < str.length(), with a ≤ to the left and a < to the right. That is appropriate, because str.length() is not a valid position. Such bounds are called asymmetric.

In this case, it is not a good idea to use symmetric bounds:

```
for (int i = 0; i <= str.length() - 1; i++) // Use < instead
```

The asymmetric form is easier to understand.

## Programming Tip 4.3
### Count Iterations

Finding the correct lower and upper bounds for an iteration can be confusing. Should you start at 0 or at 1? Should you use == or < in the termination condition?

Counting the number of iterations is a very useful device for better understanding a loop.

Counting is easier for loops with asymmetric bounds. The loop

```
for (int i = a; i < b; i++)
```

is executed b - a times. For example, the loop

```
for (int i = 0; i < 10; i++)
```

runs ten times, with values 0, 1, 2, 3, 4, 5, 6, 7, 8, and 9.

```
for (int i = a; i <= b; i++)
```

is executed b - a + 1 times. That "+1" is the source of many programming errors.

```
for (int i = 0; i <= 10; i++)
```

runs 11 times. Maybe that is what you want; if not, start at 1 or use < 10.

One way to visualize this "+1" error is by looking at a fence. Each section has one fence post to the left, and there is a final post on the right of the last section. Forgetting to count the last value is often called a "fence post error".

![](img/d61019b035dd82beb581604273c0ee6b_183_0.png)

> How many posts do you need for a fence with four sections? It is easy to be "off by one" with problems such as this one.

## 4.4 The do Loop

> The do loop is appropriate when the loop body must be executed at least once.

Sometimes you want to execute the body of a loop at least once and perform the loop test after the body is executed. The do loop serves that purpose:

```
do
{
    statements
}
while (condition);
```

The body of the do loop is executed first, then the condition is tested.

Some people call such a loop a *post-test* loop because the condition is tested after completing the loop body. In contrast, while and for loops are *pre-test* loops. In those loop types, the condition is tested before entering the loop body.

A typical example for such a loop is input validation. Suppose you ask a user to enter a value < 100. If the user didn’t pay attention and entered a larger value, you’d ask again, until the value is correct. Of course, you cannot test the value until the user has entered it. This is a perfect fit for the do loop (see Figure 5):

```
int value;
do
{
    cout << "Enter a value < 100: ";
    cin >> value;
}
while (value >= 100);
```

Here, we assume that the user will enter an integer. You saw in Section 3.8 how to exit the program if a user fails to enter an integer. Special Topic 4.1 shows how to recover from such an error.

![](img/d61019b035dd82beb581604273c0ee6b_184_0.png)

**Figure 5**  Flowchart of a do Loop

## EXAMPLE CODE

See sec04 of your companion code for a program that illustrates the use of the do loop for input validation.

![](img/d61019b035dd82beb581604273c0ee6b_184_1.png)

## Programming Tip 4.4
### Flowcharts for Loops

In Section 3.5, you learned how to use flowcharts to visualize the flow of control in a program. There are two types of loops that you can include in a flowchart; they correspond to a while loop and a do loop in C++. They differ in the placement of the condition—either before or after the loop body.

![](img/d61019b035dd82beb581604273c0ee6b_185_0.png)

![](img/d61019b035dd82beb581604273c0ee6b_185_1.png)

As described in Section 3.5, you want to avoid “spaghetti code” in your flowcharts. For loops, that means that you never want to have an arrow that points inside a loop body.

## 4.5 Processing Input

In the following sections, you will learn how to read and process a sequence of input values.

### 4.5.1 Sentinel Values

A sentinel value denotes the end of a data set, but it is not part of the data.

Whenever you read a sequence of inputs, you need to have some method of indicating the end of the sequence. Sometimes you are lucky and no input value can be zero. Then you can prompt the user to keep entering numbers, or 0 to finish the sequence. If zero is allowed but negative numbers are not, you can use −1 to indicate termination. A value that serves as a signal for termination is called a sentinel.

Let’s put this technique to work in a program that computes the average of a set of salary values. In our sample program, we will use −1 as a sentinel. An employee would surely not work for a negative salary, but there may be volunteers who work for free.

Inside the loop, we read an input. If the input is not −1, we process it. In order to compute the average, we need the total sum of all salaries, and the number of inputs.

```
while ( . . .)
{
    cin >> salary;
```

![](img/d61019b035dd82beb581604273c0ee6b_185_2.png)

© Rho... Stockphoto.
In the military, a sentinel guards a border or passage. In computer science, a sentinel value denotes the end of an input sequence or the border between input sequences.

```
if (salary != -1)
{
    sum = sum + salary;
    count++;
}
```

We stay in the loop while the sentinel value is not detected.

```
while (salary != -1)
{
    . . .
}
```

There is just one problem: When the loop is entered for the first time, no data value has been read. Be sure to initialize salary with some value other than the sentinel:

```
double salary = 0; // Any value other than -1 will do
```

Alternatively, use a do loop

```
do
{
    . . .
}
while (salary != -1)
```

The following program reads inputs until the user enters the sentinel, and then computes and prints the average.

# sec05/sentinel.cpp

```
#include <iostream>
using namespace std;

int main()
{
    double sum = 0;
    int count = 0;
    double salary = 0;
    cout << "Enter salaries, -1 to finish: ";
    while (salary != -1)
    {
        cin >> salary;
        if (salary != -1)
        {
            sum = sum + salary;
            count++;
        }
    }
    if (count > 0)
    {
        double average = sum / count;
        cout << "Average salary: " << average << endl;
    }
    else
    {
        cout << "No data" << endl;
    }
    return 0;
}
```

## Special Topic 4.1
### Clearing the Failure State

![](img/d61019b035dd82beb581604273c0ee6b_188_0.png)

When an input operation has failed, all further input operations also fail. Consider the doLoop.cpp program in Section 4.4 in which a user is prompted to enter a value that is not negative. Suppose the user enters a value that is not an integer, such as the string zero.

```
cin >> value;
```

sets cin to the failed state. If you want to give the user another chance to enter a value, you need to clear the failed state, by calling the clear member function. You also need to read and discard the offending item:

```
cin.clear();
string item;
cin >> item;
```

Now the user can try again. Here is an improved version of the do loop:

```
do {
  cout << "Enter a number >= 0: ";
  cin >> value;
  if (cin.fail()) {
    // Clear the failed state
    cin.clear();
    // Read and discard the item
    string item;
    cin >> item;
    // Set to an invalid input
    value = -1;
  }
} while (value < 0);
```

Note that we set value to an invalid input if the input was not a number, in order to enter the loop once more.

Here is another situation in which you need to clear the failed state. Suppose you read two number sequences, each of which has a letter as a sentinel. You read the first sequence:
