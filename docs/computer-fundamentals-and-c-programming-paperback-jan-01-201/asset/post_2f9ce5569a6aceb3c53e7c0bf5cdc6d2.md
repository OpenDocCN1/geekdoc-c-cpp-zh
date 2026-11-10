
**Tip:** Always look for potential errors right at the beginning of the program. It’s pointless proceeding with program execution with erroneous data. Use the `if` statements to check for them and then use `return` with specific values to prematurely terminate the program.

### 7.7 MULTI-WAY BRANCHING WITH `if-else-if` LADDER

Nothing prevents us from using a second `if` statement (in any form) inside another `if` statement. When the second `if` is inserted in the “if” section, we have a *nested if* structure (`if-if-else`). When the same is done in the “else” section, we have a *ladder* (`if-else-if`) instead. Both nested and ladder structures belong to the domain of multi-way decision making. The nested form is discussed in Section 7.10. The ladder structure is discussed here (Fig. 7.3).

```c
if (expression is true)
    statement;
else if (expression is true)
    statement;
    ...
else
    statement;
```

```c
if (expression is true) {
    statements;
    ...
}
else if (expression is true) {
    statements;
    ...
}
...
else {
    statements;
    ...
}
```

**FIGURE 7.3** The Ladder `if-else-if` Statement (Form 3)

The test on the control expression is carried out sequentially from the top downwards, and terminates as soon as it evaluates to true. The last `else` statement takes care of “the rest” and is executed only when all of the previous tests fail. C imposes no restriction on the number of `else-if` sections that can be used in this manner.

Let’s now use this construct to compute the tariff for the 4G Internet service offered by a mobile operator. The tariff is Rs 255 for up to 1 GB, Rs 455 for up to 2 GB, Rs 755 for up to 4 GB and Rs 995 thereafter (simplified from live data). This logic is easily implemented using the `if-else-if` form:

```c
if (usage <= 1)
    tariff = 255;
else if (usage <= 2)
    tariff = 455;
else if (usage <= 4)
    tariff = 755;
else
    tariff = 995;
```

> “The rest”

This chained construct uses three different relational expressions that enable the variable `tariff` to have one of four possible values. When using constructs that implement multi-way branching, you must ensure that the expressions are mutually exclusive. This means that two expressions must never evaluate to true in a single traversal of the structure.

```c
/* irctc_refund.c: Computes refund amount on ticket cancellation. Negative
   value for hours_left is valid. Maximum price of ticket = Rs 10,000 */
#include <stdio.h>
int main(void)
{
    short hours_left, rate;
    float ticket_price, refund_amount;
    printf("Enter price of ticket: ");
    scanf("%f", &ticket_price);
    printf("Number of hours before train departure: ");
    scanf("%hd", &hours_left);
    if (ticket_price <= 0) {
        printf("Price can't be negative\n");
        return 1;
    }
    else if (ticket_price > 10000) {
        printf("Price can't exceed Rs 10,000.\n");
        return 1;
    }
    else if (hours_left > 48)
        rate = 0;
    else if (hours_left > 6)
        rate = 25;
    else if (hours_left > -2)              /* 2 hours after departure */
        rate = 50;
    else
        rate = 100;                         /* No refund */
    refund_amount = ticket_price * (100 - rate) / 100;
    printf("Refund amount = %.2f\n", refund_amount);
    return 0;
}
```

| PROGRAM 7.3: `irctc_refund.c` |
| --- |
| Enter price of ticket: **11000**<br>Number of hours before train departure: **45**<br>Price can't exceed Rs 10,000. |
| Enter price of ticket: **1000**<br>Number of hours before train departure: **4**<br>Refund amount = 500.00 |
| Enter price of ticket: **1000**<br>Number of hours before train departure: **-1**<br>Refund amount = 500.00 |

PROGRAM OUTPUT: `irctc_refund.c`

### 7.8 irctc_refund.c: COMPUTES TRAIN TICKET CANCELLATION CHARGES

Program 7.3 computes the ticket cancellation charges of the IRCTC railway reservation system. This charge, computed as a percentage of the total fare, depends on the number of hours left for departure of a train. The program takes the ticket price and number of hours as input and displays the refund amount. The following table shows the cancellation charges:

| *Cancellation Time* | *Cancellation charge* |
| --- | --- |
| More than 48 hours before departure | 0% |
| Between 6 and 48 hours before departure | 25% |
| Less than 6 hours before departure and up to 2 hours *after* departure | 50% |
| More than 2 hours *after* departure | 100% |

The maximum price of a ticket is set to Rs 10,000. The program uses an `if-else-if` ladder construct both to validate the input and to compute the cancellation charge. Because cancellation is also permitted up to two hours *after* departure, the variable `hours_left` turns negative in the last `else-if` section of the construct.

Refer to the example on 4G Internet tariffs that was presented prior to this program. The control expression there used the same variable name (`usage`) throughout the `if-else` construct. However, this construct in the current program uses two different variables (`ticket_price` and `hours_left`) in the control expressions. Even though we managed to do everything in one place, the first invocation demonstrates that it was not the right thing to do. The validation check on `ticket_price` should have been conducted before taking input for `hours_left`.

### 7.9 atm_operation.c: CHECKS PIN BEFORE DELIVERY OF CASH

Program 7.4 represents an ATM cash-dispensing application that uses the `if-else-if` ladder structure. The program validates the PIN (a code) that you input and allows withdrawal of an amount not exceeding Rs 20,000. The entire code section runs in a loop, so the user has unlimited chances to key in data. This program has a number of important features, so spend some time to study it in depth.

The program uses the construct `while (1)` to set up an infinite loop, one that never terminates. You may not know much about loops, but you surely know that the expression `(1)` is always true. The loop will thus never terminate unless some statement inside the loop forces an exit. Here, either of the `return` statements forces termination of the loop.

There are two `if-else-if` ladder structures, one nested inside the other. The “outer” one handles PIN code validation. The PIN is accepted only if it comprises four digits and matches the symbolic constant `USER_PIN`. If validation fails, the remaining statements are ignored and execution “falls through” to hit the curly brace that pairs with the opening brace of the `while` loop. The entire set of instructions are then repeated for the user to re-enter the PIN.

When the program has successfully validated the PIN, control moves on to the “inner” ladder which prompts for the amount. A value of 0 for `amount` provides an escape route for the program to terminate using `return 1;`. The program also terminates when `amount` is assigned a valid value.

**Note:** The `return 0;` statement at the bottom of the program is never executed because the program exits through the paths provided by the other `return` statements placed in the inner ladder. This `return` statement placed at the bottom should be removed.

### 7.10 MULTI-WAY BRANCHING WITH NESTED `if` (`if-if-else`)

We have seen the insertion of an `if-else` section in the `else` part of the main `if` statement. When the same section is inserted in the main `if` part itself (Fig. 7.4), we have a nested `if` (`if-if-else`) structure. Like with the ladder, this is not a separate feature of the language but is derived from the `if` syntax.

![](img/d75612dcf3ab36327142238ab5bb21d8_243_0.png)

**FIGURE 7.4** The Nested `if-if-else` Statement (Form 4)

The figure shows the indentation you must adopt when using nested `if` structures. Without proper indentation, it is easy to visually pair an `if` with the wrong `else`. The pairing scheme is quite simple: The innermost `if` pairs with the innermost `else`, the immediate outer `if` pairs with the immediate outer `else`, and so on until the outermost `if` pairs with the outermost `else`. The symmetry breaks down when you drop an `else` for one of the `ifs`, but more of that soon.

Let’s look at a simple example that demonstrates the usefulness of this derived construct. Consider the need to print the sum of three positive integers obtained from user input, but only after validation. Here’s the code snippet that handles the logic:

```c
if (a > 0)
    if (b > 0)
        if (c > 0)

            /* Cleared the validity check */
            printf("Sum of three integers = %d\n", a + b + c);
        else
            printf("c is not a positive integer\n");
    else
        printf("b is not a positive integer\n");
else
    printf("a is not a positive integer\n");
```
