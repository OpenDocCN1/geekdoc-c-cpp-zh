
- Next, the *for* statement increments the control variable `counter` using the expression `++counter`, then re-tests the loop-continuation condition. The control variable is now equal to 2, so the condition is still *true*, and the *for* statement executes its `printf` statement again.
- This process continues until the control variable `counter` becomes 6. At this point, the loop-continuation condition is *false* and iteration terminates.

The program continues executing with the first statement after the *for* (line 12).

```c
1  // fig04_02.c
2  // Counter-controlled iteration with the for statement.
3  #include <stdio.h>
4  
5  int main(void) {
6     // initialization, iteration condition, and increment
7     // are all included in the for statement header.
8     for (int counter = 1; counter <= 5; ++counter) {
9        printf("%d ", counter);
10   }
11   
12   puts(""); // outputs a newline
13 }
```

```text
1  2  3  4  5
```

**Fig. 4.2** | Counter-controlled iteration with the *for* statement.

### *for* Statement Header Components

The following diagram takes a closer look at Fig. 4.2’s *for* statement, which specifies each of the items needed for counter-controlled iteration. If there’s more than one statement in the *for*’s body, braces are required. As with the other control statements, always place a *for* statement’s body in braces, even if it has only one statement.

![](img/43d318ad505997c339a3ea78d716d162_192_0.png)

### Control Variables Defined in a *for* Header Exist Only Until the Loop Terminates

When you define the control variable in the *for* header before the first semicolon (;), as in line 8 of Fig. 4.2:

```c
for (int counter = 1; counter <= 5; ++counter) {
```

the control variable exists only until the loop terminates. So, attempting to access the control variable after the `for` statement’s closing right brace (`}`) is a compilation error.

### Off-By-One Errors

If we had written the loop-continuation condition `counter <= 5` as `counter < 5`, then the loop would be executed only four times. This is a common logic error called an off-by-one error. Using a control variable’s final value in a `while` or `for` statement condition and using the `<=` relational operator can help avoid off-by-one errors. To print the values 1 to 5, for example, the loop-continuation condition should be `counter <= 5` rather than `counter < 6`.

### General Format of a for Statement

The general format of the `for` statement is

```c
for (initialization; loopContinuationCondition; increment) {
    statement
}
```

where

- `initialization` names the loop’s control variable and provides its initial value;
- `loopContinuationCondition` determines whether the loop should continue executing, and
- `increment` modifies the control variable’s value after executing the `statement` so that the loop-continuation condition eventually becomes `false`.

The two semicolons in the `for` header are required. If the loop-continuation condition is initially `false`, the program does not execute the `for` statement’s body. Instead, execution proceeds with the statement following the `for`.

Infinite loops occur when the loop-continuation condition never becomes `false`. To prevent infinite loops, ensure that you do not place a semicolon immediately after a `while` statement’s header. In a counter-controlled loop, ensure that you increment (or decrement) the control variable so the loop-continuation condition eventually becomes `false`. In a sentinel-controlled loop, ensure that the sentinel value is eventually input.

### Expressions in the for Statement’s Header Are Optional

All three expressions in a `for` header are optional. If you omit the `loopContinuationCondition`, the condition is always true, thus creating an infinite loop. You might omit the `initialization` expression if the program initializes the control variable before the loop. You might omit the `increment` expression if the program calculates the increment in the loop’s body or if no increment is needed.

### Increment Expression Acts Like a Standalone Statement

The `for` statement’s `increment` acts like a standalone C statement at the end of the `for`’s body. So, the following are all equivalent in a `for` statement’s increment expression:

```c
counter = counter + 1
counter += 1
++counter
counter++
```

The increment in a for statement's increment expression may be negative, in which case it's a decrement, and the loop counts downward.

### Using a for Statement's Control Variable in the Statement's Body

Programs frequently display the control-variable value or use it in calculations in the loop body, but this use is not required. The control variable is commonly used to control iteration without being mentioned in the for statement's body. Although the control variable's value can be changed in a for loop's body, avoid doing so, because this practice can lead to subtle errors. It's best not to change it.

### for Statement Flowchart

Below is the flowchart for the for statement in Fig. 4.2:

![](img/43d318ad505997c339a3ea78d716d162_194_0.png)

This flowchart makes it clear that the initialization occurs once, and the increment occurs after the body statement each time it's performed.

### Self Check

- 1 (True/False) When you define the control variable in the for header before the first semicolon (;), the control variable exists only until the loop terminates.
  - Answer: True.
- 2 (Multiple Choice) Which of the following statements a), b) or c) is true?
  - a) The for statement header specifies each of the items needed for counter-controlled iteration with a control variable.
  - b) If there's more than one statement in a for's body, braces are required.
  - c) You should always place a control statement's body in braces, even if it has only one statement.
  - d) All of the above statements are true.
  - Answer: d.

## 4.5 Examples Using the For Statement

The following examples show ways to vary the control variable in a for statement.

- 1. Vary the control variable from 1 to 100 in increments of 1.

    ```c
    for (int i = 1; i <= 100; ++i)
    ```
- 2. Vary the control variable from 100 to 1 in increments of −1 (i.e., decrements of 1).

    ```c
    for (int i = 100; i >= 1; --i)
    ```
- 3. Vary the control variable from 7 to 77 in increments of 7.

    ```c
    for (int i = 7; i <= 77; i += 7)
    ```
- 4. Vary the control variable from 20 to 2 in increments of −2.

    ```c
    for (int i = 20; i >= 2; i -= 2)
    ```
- 5. Vary the control variable over the values 2, 5, 8, 11, 14 and 17.

    ```c
    for (int j = 2; j <= 17; j += 3)
    ```
- 6. Vary the control variable over the following sequence of values: 44, 33, 22, 11, 0.

    ```c
    for (int j = 44; j >= 0; j -= 11)
    ```

### Application: Summing the Even Integers from 2 to 100

Figure 4.3 uses the for statement to sum the even integers from 2 to 100. Each loop iteration (lines 8–10) adds the control variable number’s current value to the sum.

```c
// fig04_03.c
// Summation with for.
#include <stdio.h>

int main(void) {
    int sum = 0; // initialize sum

    for (int number = 2; number <= 100; number += 2) {
        sum += number; // add number to sum
    }

    printf("Sum is %d\n", sum);
}
```

```text
Sum is 2550
```

**Fig. 4.3** | Summation with for.

### Application: Compound-Interest Calculations

The next example computes compound interest using the for statement. Consider the following problem statement:

> *A person invests $1000.00 in a savings account yielding 5% interest. Assuming all interest is left on deposit in the account, calculate and print the amount of money in the account at the end of each year for 10 years. Use the following formula for determining these amounts:*
>
> a = p(1 + r)^n
>
> where
> - p is the original amount invested (i.e., the principal, $1000.00 here),
> - r is the annual interest rate (for example, .05 for 5%),
> - n is the number of years, which is 10 here, and
> - a is the amount on deposit at the end of the n^th year.

The solution (Fig. 4.4) uses a counter-controlled loop to perform the same calculation for each of the 10 years the money remains on deposit. The for statement executes its body 10 times, varying a control variable from 1 to 10 in increments of 1. C does not include an exponentiation operator, so we use the Standard Library function pow (line 17) for this. The call pow(x, y) calculates x raised to the yth power. The function takes two arguments of data type double. When it completes its calculation, pow returns (that is, gives back) a double value, which we then multiply by principal (line 17).

```c
// fig04_04.c
// Calculating compound interest.
#include <stdio.h>
#include <math.h>

int main(void) {
    double principal = 1000.0; // starting principal
    double rate = 0.05; // annual interest rate

    // output table column heads
    printf("%4s%21s\n", "Year", "Amount on deposit");

    // calculate amount on deposit for each of ten years
    for (int year = 1; year <= 10; ++year) {

        // calculate new amount for specified year
        double amount = principal * pow(1.0 + rate, year);

        // output one table row
        printf("%4d%21.2f\n", year, amount);
    }
}
```

| Year | Amount on deposit |
|------|-------------------|
| 1 | 1050.00 |
| 2 | 1102.50 |
| 3 | 1157.63 |
| 4 | 1215.51 |
| 5 | 1276.28 |
| 6 | 1340.10 |
| 7 | 1407.10 |
| 8 | 1477.46 |
| 9 | 1551.33 |
| 10 | 1628.89 |

**Fig. 4.4** | Calculating compound interest.
