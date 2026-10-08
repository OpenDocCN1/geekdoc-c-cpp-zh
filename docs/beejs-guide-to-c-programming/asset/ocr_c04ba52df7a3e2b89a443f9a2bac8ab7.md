# Chapter 3. Variables and Statements

i = 10;

// this is executed once, because the loop condition is not checked until
// after the body of the loop runs:

```
do {
    printf("do-while: i is %d\n", i);
    i++;
} while (i < 10);
```

printf("all done!\n");

Note that in all cases, the loop condition is false away. So in while, the loop fails, and the following block of code is never executed. With the do-while, however, the condition is checked after the block of code executes, so it always executes at least once. In this case, it prints the message, increments i, then fails the condition, and continues to the "All done!" output.

The moral of this story is: if you want the loop to execute at least once, no matter what the loop condition, use do-while.

All these examples might have been better done with a for loop. Let's do something less deterministic-repeat until a random number comes up!

```
#include <stdio.h> // For printf
#include <stdlib.h> // For rand

int main(void) {
    int r;

     {
        r = rand() % 100; // Get a random number between 0 and 99
        printf("%d\n", r);
    } while (r != 37); // Repeat until 37 comes
}
```

Side note: did you run it more than once? If you did, you would notice the same sequence of numbers came up again. And again? Again? This is because rand() is a pseudorandom number generator that must be seeded with a different number in order to generate a different sequence. Look up the rand() function for more details.

# 3.3.4 The statement

Welcome to one of the most popular loops in the world! For your loop!

This is a great loop if you know how many times you want to loop in advance.

You could do the same thing using just a while loop, but the for loop can help keep the code cleaner.

Here are two pieces of equivalent code—note how the for loop is just a more compact representation:

```
// Print numbers between 0 and 9, inclusive...
```

```
// Using a while statement:
```

```
i = 0;
```

> https://beej.us/guide/bgclr/html/split/stdlib.html#man-rand