In this version, i is initialized before the loop begins, rather than as part of the **for**. Normally, you will want to initialize the loop control variable inside the **for**. Placing the initialization outside of the loop is generally done only when the initial value is derived through a complex process that does not lend itself to containment inside the **for** statement.

# The Infinite Loop

You can create an *infinite loop* (a loop that never terminates) using the **for** by leaving the conditional expression empty. For example, the following fragment shows the way many C# programmers create an infinite loop:

```
for(;;) // intentionally infinite loop
{
    //...
}
```

This loop will run forever. Although there are some programming tasks, such as operating system command processors, that require an infinite loop, most "infinite loops" *are* really just loops with special termination requirements. (See "Using **break** to Exit a Loop," later in this chapter.)

# Loops with No Body

In C#, the body associated with a **for** loop (or any other loop) can be empty. This is because a *empty statement* is syntactically valid. Bodyless loops are often useful. For example, the following program uses a bodyless loop to sum the numbers 1 through 5:

```
// The body of a loop can be empty.

using System;

class Empty3 {
    static void Main() {
        int i;
        int sum = 0;

        // Sum the numbers through 5.
        for(i = 1; i <= 5; sum += i++) ;

        Console.WriteLine("Sum is " + sum);
    }
}
```

The output from the program is shown here:

```
Sum is 15
```

Notice that the summation process is handled entirely within the **for** statement, and no body is needed. Pay special attention to the iteration expression:

```
sum += i++
```

Don't be intimidated by statements like this. They are common in professionally written C# programs and are easy to understand if you break them down into their parts. In words,