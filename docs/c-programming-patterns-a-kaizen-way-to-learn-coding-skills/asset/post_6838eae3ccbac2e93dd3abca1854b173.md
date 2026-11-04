
## ForLoopIncrement.C

```c
#include <stdio.h>

int main() {

    for ( int counter = 1 ; counter <= 5 ; counter ++ ){

        printf("%d\n",counter);//print to console

    }

    return 0;

}
```

### Output

```
1
2
3
4
5
```

Case b: Changing the *loop-condition* counter <= 5 to counter < 5, and let's see the result.

## ForLoopIncrement1.C

```c
#include <stdio.h>

int main() {

    for ( int counter = 1 ; counter < 5 ; counter ++ ){

        printf("%d\n",counter);//print to console

    }

    return 0;

}
```

### Output

```
1
2
3
4
```

It printed from 1 to 4.

## Case c: Let's modify ForLoopIncrement1.c keeping loop-condition ( `counter < 5` ) same and yet still should print 1 to 5.

## ForLoopIncrement2.C

```c
#include <stdio.h>

int main() {

    for ( int counter = 0 ; counter < 5 ; counter ++ ){

        int result = counter + 1; //add 1 to the counter

        printf("%d\n",result);//print to console
    }

    return 0;

}
```

### Output

```text
1
2
3
4
5
The variable counter started with the value 0 instead of 1.
```

## Case d: Let's express range(min_val, max_val) where min_val < max_val with **counter-update** decremented value 1.

The for-loop can be expressed as;

```c
for (int *variable_name* = max_val; *variable_name* >= min_val ; *variable_name* --){

    statement(s);

}
```

To print numbers 1 to 5 in descending order with **counter-update** decremented value 1, then the ***for-loop*** can be expressed as;

Hence decrement *for-loop* can be expressed as the given following flow chart.

![](img/67765455776ddeb6395161cd553ecd87_86_0.png)

## ForLoopDecrement.c

```c
#include <stdio.h>
int main() {
    for ( int counter = 5 ; counter >= 1; counter -- ){
        printf("%d\n", counter ); //print to console
    }
    return 0;
}
```

### Output

5
4
3
2
1

## For-loop with {break} and {continue} keywords

- “break” keyword within the for-loop stops further repetition of loop when condition for “break,” statement is reached.
- It's similar like a moving car stops when driver applies the break.
- “continue” keyword bounce back control of the executing program to the for-loop to continue without giving chance to execute further statement(s) after the continue; statement.

```c
ForLoopContinueNext.c
#include <stdio.h>

int main() {
    for( int cnt = 1 ; cnt <= 10 ; cnt ++ ) {
        if( cnt <= 3 ) {
            printf("keyword{continue} is throwing ");
            printf("control of program back.\n");
            continue;
        }
        printf("Please Join Us...!!!\n");
        if( cnt == 5 ) {
            printf("keyword{break} at cnt = %d\n", cnt);
            break;
        }
        printf("Please look back...\n" );
    }
    return 0;
}
```

### Output

keyword(continue) is throwing control of program back.
keyword(continue) is throwing control of program back.
keyword(continue) is throwing control of program back.
Please Join Us...!!!
Please look back...
Please Join Us...!!!
keyword(break) at cnt = 5

## Nested for-loop/Inner for-loop

We have previously seen examples of for-loop that have if-statements or any other simple statements. Instead of simple if- statement within for-loop we place another for-loop then how the things will be. For example;

```c
for ( int counter = 5 ; counter >= 1; counter -- ){
        // print the variable counter's value
        printf ("%d\n", counter ); //statement1
        printf ("%d\n", 2*counter ); //statement2
        printf ("%d\n", 3*counter ); //statement3
}
```

We know that these considered statements will get execute in order. Firstly statement1 will get executed, then statement2 and lastly statement3 will get executed. All these statements will repeat 5 times when we execute the considered piece of program. If we place another for-loop instead of any single statement, the major style of work doesn’t change. We need to think in way that **inner for-loop** itself is like some other single **programming statement**. Whenever control of a program starts executing programming statements in a sequence and finds any **inner for-loop**, it will then fully executes inner for-loop and then executes next statement(s) if there are any available.

For example;

```c
for ( int counter = 5 ; counter >= 1; counter -- ){
    // print the variable counter's value
    printf ("%d\n", counter ); //statement1
    //The for-loop is a single statement
    for(int inner = 1 ; inner <= 5; inner ++){
        printf ("%d\n", inner );
    }
    printf ("%d\n", 3* counter ); //statement3
}
```

> > Please treat
> > nested for-loop
> > as a single
> > programming
> > statement

Now as usual **statement1** gets completed first. Then inner for-loop with 5 times repetitions will get executed completely and finally **statement3** will get executed. All these **three statements** will repeat 5 times as suggested by the structure of outer for-loop. Whenever a for-loop is placed within the code block of another for-loop is known as **inner for-loop** or **nested for-loop**.

The inner for-loop will **restart from the beginning** for every new value of a outer for-loop.

It is easy to follow this concept if we try to relate it with time piece clock with following assumptions;

**Inner Loop →** It’s like a “seconds” hand in a clock
**Outer Loop →** It’s like a “minute” hand in a clock

In a clock when “seconds” hand completes one cycle then only afterwards “minute” hand will get updated by counter value 1 and not before.

![](img/67765455776ddeb6395161cd553ecd87_88_0.png)

The **inner for-loop will execute completely before every new counter value of outer for-loop** to continue repetition depends upon it’s loop-condition.

![](img/67765455776ddeb6395161cd553ecd87_89_0.png)

## NestedForLoop.c

```c
#include <stdio.h>
int main() {
    for( int out = 1 ; out <= 2 ; out++ ) {
        printf("OUTER count No.%d\n", out);
        // nested for-loop: always re-starts and finishes
        // completely for every new value of outer for-loop.
        for( int in = 1; in <= 3; in++ ) {
            printf(" <INNER> count No.%d\n", in );
        }
    }
    return 0;
}
```

### Output

OUTER count No.1
<INNER> count No.1
<INNER> count No.2
<INNER> count No.3
OUTER count No.2
<INNER> count No.1
<INNER> count No.2
<INNER> count No.3

## Nested Loop: Beginner Programmer's Best Friend

Best friend is a person not only who appreciates our good quality but also gives reality check by showing our weaknesses or mistakes whenever it is required. Nested loop plays such best friend's role while learning programming logic and it also gives a reality check how much true is our programming logic. This is my personal opinion that **practising a programming logic just by juggling with numbers is not a good idea** and specially for a person who had a less or no inclination towards higher school mathematics. Many of them feel bored to practice on such mathematical problems in order to learn skill of programming logic.

Everybody is different and everyone has a different buffer of patience and pace of learning. There should be a simple to understand approach. Any beginner who want to learn/improve programming should be able to do it with his own learning pace on the backdrop of minimal technical stuff.

It is broadly three-step learning process on pictorial based exercises so that beginners get comfortable in the programming.

- **Step1.** Clarity about how logical condition is to be explored.
- **Step2.** Clarity about how nested loop works. This is our next major hands-on training.
- **Step3.** Finding a scope to improve implemented program so that programming logic can be further simplified. Looking for alternate possible solutions.

After going through these three steps, anyone will be in a confident position to learn and explore advanced features of programming language.

## *Why nested loops are such an important deal?*

The outer for-loop and inner for-loop, each one are used for outputting data in different direction horizontally and vertically to give a 2-dimensional output. Usually outer for-loop moves the control vertically and inner for-loop outputs the data horizontally. This gives a grid kind of output. This particular feature of looping can be utilized to perfect the imagination of the learner. Yes, logic building is a skill and can be developed using simple maths and common sense. It's not a must for a person to be very good in maths in order to be a successful programmer or software developer. If a learner is able to imagine the behaviour of outer and nested loop correctly, the person will gain enough confidence that he/she can code.

The first and foremost requirement for any subject related teaching is to first create interest about the subject among the student or learner group. If a learner gets deeply connected with the subject than rest of the learning with be without burden. Learner will enjoy learning and this course is
