
## 5.1 The while Statement

A while statement is a general repetition statement that can be used in a variety of programming situations. It has this general form:

```
while (expression)
statement;
```

The expression in parentheses is evaluated in exactly the same manner as one in an if-else statement; the difference is in how the expression is used. As you have seen, when the expression in an if-else statement is true (has a non-zero value), the statement following the expression is executed once. In a while statement, the statement following the expression is executed repeatedly as long as the expression evaluates to a non-zero value. Naturally, this means that somewhere in the while statement must be a statement altering the tested expression's value. As you'll see, this is indeed the case. For now, however, considering just the expression and the statement following the parentheses, the computer uses this process in evaluating a while statement:

- 1. Test the expression
- 2. If the expression has a non-zero (true) value
  - a. execute the statement following the parentheses
  - b. go back to Step 1
- else
- exit the while statement and execute the next executable statement following the while statement

Notice that Step 2b forces program control to be transferred back to Step 1. This transfer of control back to the start of a while statement to reevaluate the expression is what forms the program loop. The while statement literally loops back on itself to recheck the expression until it evaluates to zero (becomes false). This rechecking means the loop must contain a provision that permits altering the tested expression's value. As you'll see, this provision is indeed made.

Figure 5.1 shows the looping process a while statement produces. A diamond shape is used to show the two entry and two exit points required in the decision part of the while statement.

To make this looping process more tangible, consider the relational expression count <= 10 and the statement cout << count;. Using these elements, you can write the following valid while statement:

```
while (count <= 10)
    cout << count;
```

Although this statement is valid, the alert reader will realize that it creates a situation in which the cout statement is called forever (or until you stop the program) or not called at all. Here's why this happens: If count has a value less than or equal to 10 when the expression is first evaluated, a call to cout is made. The while statement then automatically loops back on itself and retests the expression. Because you haven't changed the value stored in count, the expression is still true, and another call to cout is made. This process continues forever, or until the program containing this statement is stopped prematurely by the user. However, if

count starts with a value greater than 10, the expression is false to begin with, and the call to cout is never made.

![](img/e9bf940282dfb289356f077151cc69dd_200_0.png)

### Figure 5.1 Anatomy of a while loop

How do you set an initial value in count to control what the while statement does the first time the expression is evaluated? The answer, of course, is to assign values to each variable in the tested expression before the while statement is encountered. For example, the following sequence of instructions is valid:

```
count = 1;
while (count <= 10)
    cout << count << " ";
```

Using this sequence of instructions ensures that count starts with a value of 1. You could assign any value to count in the assignment statement. What's important is to assign some value. In practice, the assigned value depends on the application.

You must still change the value of count so that you can finally exit the while statement. Doing so requires an expression such as count = count + 1 to increment the value of count each time the while statement is executed. The fact that a while statement provides

for repetition of a single statement doesn't prevent including an additional statement to change the value of count. All you have to do is replace the single statement with a compound statement, as in this example:

```
count = 1;      // initialize count
while (count <= 10)
{
    cout << count << " ";
    count++;       // increment count
}
```

Note that, for clarity, each statement in the compound statement is placed on a different line. This format is consistent with the convention adopted for compound statements in Chapter 4.

Now analyze the preceding sequence of instructions. The first assignment statement sets count equal to 1. The while statement is then entered, and the expression is evaluated for the first time. Because the value of count is less than or equal to 10, the expression is true, and the compound statement is executed. The first statement in the compound statement uses the cout object to display the value of count. The next statement adds 1 to the value currently stored in count, making this value equal to 2. The while statement then loops back to retest the expression. Because count is still less than or equal to 10, the compound statement is executed again. This process continues until the value of count reaches 11. Program 5.1 shows these statements in an actual program.

### Program 5.1

```
#include <iostream>
using namespace std;

int main()
{
    int count;

    count = 1;      // initialize count
    while (count <= 10)
    {
        cout << count << " ";
        count++;       // increment count
    }

    return 0;
}
```

This is the output for Program 5.1:

1 2 3 4 5 6 7 8 9 10

Note that there's nothing special about the name count used in Program 5.1. Any valid integer variable could have been used.

Before you look at other examples of the while statement, two comments on Program 5.1 are in order. First, the statement count++ can be replaced with any statement that changes the value of count. A statement such as count = count + 2;, for example, causes every second integer to be displayed. Second, it's the programmer's responsibility to ensure that count is changed in a way that leads to a normal exit from the while statement. For example, if you replace the expression count++ with the expression count--, the value of count never exceeds 10 and an infinite loop is created. An infinite loop is one that never ends. The computer doesn't tap you on the shoulder and say, "Excuse me. You've created an infinite loop." The program just keeps displaying numbers until you realize it isn't working as you expected.

Now that you have some familiarity with the while statement, see whether you can read and determine the output of Program 5.2.

### Program 5.2

```
#include <iostream>
using namespace std;

int main()
{
    int i;

    i = 10;
    while (i >= 1)
    {
        cout << i << " ";
        i--;  // subtract 1 from i
    }

    return 0;
}
```

The assignment statement in Program 5.2 initially sets the int variable i to 10. The while statement then checks whether the value of i is greater than or equal to 1. While the expression is true, the value of i is displayed by the cout object, and the value of i is decremented by 1. When i finally reaches 0, the expression is false, and the program exits the while statement. Therefore, Program 5.2 produces the following display when it runs:

10 9 8 7 6 5 4 3 2 1

To understand the power of the while statement, consider the task of printing a table of numbers from 1 to 10 with the numbers' squares and cubes. You can do this with a simple while statement, as shown in Program 5.3.

### Program 5.3

```
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    int num;
    cout << "NUMBER   SQUARE   CUBE\n"
         << "------   ------   ----\n";

    num = 1;
    while (num < 11)
    {
        cout << setw(3) << num << "      "
             << setw(3) << num * num << "      "
             << setw(4) << num * num * num << endl;
        num++;  // increment num
    }

    return 0;
}
```

When Program 5.3 runs, the following display is produced:

| NUMBER | SQUARE | CUBE |
| ------ | ------ | ---- |
| 1      | 1      | 1    |
| 2      | 4      | 8    |
| 3      | 9      | 27   |
| 4      | 16     | 64   |
| 5      | 25     | 125  |
| 6      | 36     | 216  |
| 7      | 49     | 343  |
| 8      | 64     | 512  |
| 9      | 81     | 729  |
| 10     | 100    | 1000 |

Note that the expression used in Program 5.3 is num < 11. For the integer variable num, this expression is exactly equivalent to the expression num <= 10. The choice of which to use is entirely up to you.

If you want to use Program 5.3 to produce a table of 1000 numbers, all you do is change the expression in the while statement from num < 11 to num < 1001. Changing the 11 to 1001 produces a table of 1000 lines—not bad for a simple five-line while statement.
