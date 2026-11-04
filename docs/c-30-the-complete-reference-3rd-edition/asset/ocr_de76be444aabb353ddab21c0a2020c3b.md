```
while(e > 0) {
    result *= 2;
    e--;
}
}

Console.WriteLine("2 to the " + i + " power is " + result);
}
```

The output from the program is shown here:

```
2 to the 0 power is 1
2 to the 1 power is 2
2 to the 2 power is 4
2 to the 3 power is 8
2 to the 4 power is 16
2 to the 5 power is 32
2 to the 6 power is 64
2 to the 7 power is 128
2 to the 8 power is 256
2 to the 9 power is 512
```

Notice that the while loop executes only when e is greater than 0. Thus, when e is 0, as it is in the first iteration of the for loop, the while loop is skipped.

# The do-while Loop

The third C# loop is the do-while. Unlike the for and the while loops, in which the condition is tested at the top of the loop, the do-while loop checks its condition at the bottom of the loop. This means that a do-while loop will always execute at least once. The general form of the do-while loop is

```
do {
    statements;
} while(condition);
```

Although the braces are not necessary when only one statement is present, they are often used to improve readability of the do-while construct, thus preventing confusion with the while. The do-while loop executes as long as the conditional expression is true.

The following program uses a do-while loop to display the digits of an integer in reverse order:

```
// Display the digits of an integer in reverse order.

using System;

class DoWhileDemo {
    static void Main() {
        int num;
        int nextdigit;

        num = 198;
```