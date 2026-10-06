# Creating Loops with the for Statement

+   * You can leave one or more portions of the for expression empty, the two semicolons are still required as placeholders to separate the three sections. Usually, you want to use all three sections because the function of the loop is clearer to someone reading your program.

Generally, you should use the for loop in the standard manner, which is a shorthand of initializing, testing, and altering a variable that defines a loop. You will learn about a similar loop, the foreach loop, when you study arrays in the next chapter.

Just as a decision or a while loop, statements in a for loop body can be blocked. For example, the for loop displays Hello and Goodbye four times each:

```
const int TIMES = 4;
for(int x = 0; x < TIMES; ++x)
{
    WriteLine("Hello");
    WriteLine("Goodbye");
}
```

Without the clauses in this code, the for loop would end after the statement that displays Hello. In other words, Hello would be displayed four times, but Goodbye would be displayed only once.

![](bbox=[0.105, 0.495, 0.148, 0.526])

Watch the video Using the for Loop.

| TWO TRUTHS & A LIE |
| :--- |
| **Creating Loops with the for Statement** |
| -------------------------------------- |
1. The following statement displays the numbers 3 through 6:
for(int x = 3; x <= 6; ++x)
WriteLine(x);
2. The following statement displays the numbers 4 through 9:
for(int x = 3; x < 9; ++x)
WriteLine(x);
3. The following statement displays the numbers 5 through 12:
for(int x = 5; x < 12; ++x)
WriteLine(x);