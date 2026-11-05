The following example will illustrate how while loops work:

```
int timer = 10;
while (timer >= 0)
{
System.Console.WriteLine("Time remaining: " + timer);
timer--;
}
```

If you will compile and execute this code, your command prompt will print this data:

```
Time remaining: 10
Time remaining: 9
Time remaining: 8
Time remaining: 7
Time remaining: 6
Time remaining: 5
Time remaining: 4
Time remaining: 3
Time remaining: 2
Time remaining: 1
Time remaining: 0
```

# The Break Operator

You can use “break” (a C# operator) to exit a loop prematurely. Programmers use this operator if they don’t want to wait for the loop’s natural termination. Basically, a loop will end once it encounters a break operator. This situation forces the program to jump to the code fragments right after the loop.

In C#, you can only use this operator inside the loop’s body. That means “break” will only work while the loop is running.

# The Do-While Loop

A do-while loop is almost identical to a while loop. The only difference between these