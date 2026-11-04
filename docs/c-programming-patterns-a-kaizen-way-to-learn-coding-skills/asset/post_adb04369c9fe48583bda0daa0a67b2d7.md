
## Case 1.

int num1 = 80;

int num2 = 40;

condition: (num1 > num2) , if (80 > 40), will evaluate to “true”

if(condition) will be “true” and executes the if-block.

![](img/67765455776ddeb6395161cd553ecd87_72_0.png)

### StatementIfElse.c

```
#include <stdio.h>

int main() {
    int num1 = 80;
    int num2 = 40;
    if( num1 > num2) {
        printf("%d is greater than %d",num1,num2);
    }else {
        printf("%d is less than or equals to %d", num1, num2);
    }
    return 0;
}
```

### Output

80 is greater than 40

## Case 2. Change the value of num1 and num2 in the program.

int num1 = 40;

int num2 = 80;

condition: (num1 > num2), if (40 >80), will evaluate to “false”

If(condition) will be “false” and executes the else-block.

![](img/67765455776ddeb6395161cd553ecd87_73_0.png)

### StatementIfElse1.c

```
#include <stdio.h>

int main() {
    int num1 = 40;
    int num2 = 80;
    if( num1 > num2) {
        printf( "%d is greater than %d", num1, num2);
    }else {
        printf( "%d is less than %d", num1, num2);
    }
    return 0;
}
```

### Output

40 is less than 80

## c) if-else if-else statement

![](img/67765455776ddeb6395161cd553ecd87_74_0.png)

The general syntax for if-else if-else statement can be given as:

```
```text
if (condition1) {
    execute statement(s)-1;          if-block
}else if(condition2) {
    execute statement(s)-2;          else-if-block
}else{
    execute statement(s)-3;          else-block
}
```
```

## Case 1.

int num1 = 80;

int num2 = 40;

condition : (num1 > num2) ,if (80 > 40), will evaluate to “true”

If(condition) will be “true” and executes the if-block.

![](img/67765455776ddeb6395161cd553ecd87_75_0.png)

### StatementIfElseIf.c

```
#include <stdio.h>
int main() {
    int num1 = 80;
    int num2 = 40;
    if( num1 > num2 ) {
        printf("%d is greater than %d",num1, num2);
    }else if( num1 < num2 ) {
        printf("%d is less than %d",num1, num2);
    }else {
        printf("%d equals to %d", num1, num2);
    }
    return 0;
}
```

### Output

80 is greater than 40

## Case 2. Change the value of num1 and num2 in the program.

int num1 = 40;

int num2 = 80;

(num1 > num2) boolean expression will evaluate to "false" and will go to next boolean expression (num1 < num2).

(num1 < num2) will evaluate to "true" as ( 40 < 80).

![](img/67765455776ddeb6395161cd553ecd87_76_0.png)

So, else if ( num1 < num2 ), else if(condition) will be "true" and executes the else if-block.

### StatementIfElseIf1.c

```c
#include <stdio.h>

int main() {

    int num1 = 40;

    int num2 = 80;

    if( num1 > num2 ) {

        printf("%d is greater than %d",num1, num2);

    }else if( num1 < num2 ) {

        printf("%d is less than %d",num1, num2);

    }else {

        printf("%d equals to %d", num1, num2);

    }

    return 0;

}
```

Output
40 is less than 80

*ProblemLadderIfElse:* A college came up with an idea to encourage CS students by refunding some percentage of their bi-semester CS Course fees. College management laid the following conditions to be eligible for the same. Moreover, if a student scored in Grade-0, will be declared failed.

- If a student scored in Grade-5, will be eligible for 35% refund of the college fees.
- If a student scored in Grade-4, will be eligible for 25% refund of the college fees.
- If a student scored in Grade-3, will be eligible for 20% refund of the college fees.
- If a student scored in Grade-2, will be eligible for 10% refund of the college fees.
- If a student scored in Grade-1, will be passed with margin.

### LadderIfElse.c

```
```c
#include <stdio.h>
int main() {
    int grade = 2;
    if(grade == 1) {
        printf("35%% fee refund.");
    }else if(grade == 2) {
        printf("25%% fee refund.");
    }else if(grade == 3) {
        printf("20%% fee refund.");
    }else if(grade == 4) {
        printf("10%% fee refund.");
    }else if(grade == 5) {
        printf("Passed with margin.");
    }else if(grade == 0) {
        printf("Failed,please retry.");
    }else {
        printf("Invalid grade ? %d", grade);
    }
    return 0;
}
//Note:- %% double percentage symbols are used to print %
```
```

### Output

25% fee refund.

It’s going to test if-conditions sequence-wise, unless and until some if-condition becomes true.

This type of many else-if is also called as ladder else-if, which is basically not a good practice.

When two or three else-if condition are used, is considered to be okay and further more else-if conditions are strongly discouraged as it reduces the code readability.

Then what is the way-out?

The answer is switch-case construct.

## d) switch-case

![](img/67765455776ddeb6395161cd553ecd87_79_0.png)

The general syntax for **switch-case statement** can be given as:

```
```
switch(expression value ?){
case expression 1:
    execute statement(s)-1;
    break;
case expression 2:
    execute statement(s)-2;
    break;
...
break;
case expression n:
    execute statement(s)-n;
    break;
default:
    // default if none of the case_expression value matched
    execute statement(s);
}// switch-case ends
next statement(s); // continue program execution
```
```

Let's convert ladder if-else statement to switch-case. The previous code LadderIfElse.c can be re-written as:

### ConvertLadderIfElseToSwitchCase.c

```
```c
#include <stdio.h>

int main() {
    int grade = 21;
    switch (grade) {
    case 1:
        printf("35% fee refund.");
        break;
    case 2:
        printf("25% fee refund.");
        break;
    case 3:
        printf("20% fee refund.");
        break;
    case 4:
        printf("10% fee refund.");
        break;
    case 5:
        printf("Passed with margin.");
        break;
    case 0:
        printf("Failed,please retry.");
        break;
    default:
        printf("Invalid grade ? %d", grade);
        break;
    }
    return 0;
}
```
```

### Output

Invalid grade ? 21

switch-case is the elegant way of dealing with ladder if-conditions.

## My Notes : programming Logic Experiences.

> > You can’t manage what you can’t measure.  
> > — Peter Drucker

Write the key points of your programming logic experiences from alphabetic exercises.

| S.No | Short Description | Description |
|---|---|---|

## About for-loop

In case of high calculation intensive data or large amount of data processing activities, human resources are not reliable in terms of accuracy and productivity as compared to computers. Nothing is automatic unless someone does it. The feature of repetitiveness helps to automate tedious data processing work amazingly efficient and accurate as compared to doing it manually. One of the repetitive control feature in a programming is known as **for statement** or **for-loop**. In a very generic way **for-loop** can be expressed as follows:

![](img/67765455776ddeb6395161cd553ecd87_82_0.png)

```
```
for (start-loop; loop-condition ; counter-update ) {
    execute statement(s);
}

next statement;
```
```

- **_start-loop_** is a simple way of initialisation of a variable and anyway from some point the process of repetitive cycle has to be get started.
- **_loop-condition_** is a logical expression which evaluates a boolean value either **_true_** or **_false._** Based on this (**_true/false_**), **_for-loop_** control structure decides whether to repeat the set of statement(s) or not.
- **_counter-update_** is a change in variable's value in a fixed smaller steps (increment/decrement) only after all statement(s) gets executed in **for-loop** block. Usually it holds strong bonding with **_start-loop_** and **_loop-condition._**

The *for-loop* helps a programmer to repeat programming statement(s) over a “range of values”.
When we talk about a range, then it must have a minimum value and a maximum value.

We will use the following notations:

| Notation | Description |
|---|---|
| *min_val* | minimum value from where the for-loop starts the repetition. |
| *max_val* | maximum value to the extent where for-loop will do the repetition. |

It means *for-loop* will operate between *min_val* and *max_val* values. We can understand this concept better by doing examples based on incrementing or decrementing *counter-update* expression of the *for-loop*.

## Basics

Here are some basic examples to get clarity about how the *for-loop* behaves.

Let’s express range [*min_val*, *max_val*] where *min_val* < *max_val* with counter-update incremental value 1. The for-loop can be expressed as;

```
for ( int variable_name = min_val ; variable_name <= max_val ; variable_name ++ ){

        statement(s);

}
```

### Case a:

Let the range be [1,5] with counter-update incremental value 1, then the for-loop can be expressed to print counter variable’s value 1 to 5 in ascending order which is as follows;

```
for ( int counter = 1 ; counter <=5 ; counter ++ ) {

        printf("%d\n", counter); //print output to console

}
```

Hence the above *for-loop* can be expressed as a flow chart which is as follows:

![](img/67765455776ddeb6395161cd553ecd87_83_0.png)
