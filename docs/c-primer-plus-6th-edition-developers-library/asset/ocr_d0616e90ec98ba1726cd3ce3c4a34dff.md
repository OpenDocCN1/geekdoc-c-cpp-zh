```
index = 0;
while (index++ < 10)
    sam = 10 * index + 2;
printf("sam = %d\n", sam);
```

```
/* fragment 2 */
index = 0;
while (index++ < 10)
{
    sam = 10 * index + 2;
    printf("sam = %d\n", sam);
}
```

In fragment 1, only the assignment statement is included in the while loop. In the absence of braces, a while statement runs from the while to the next semicolon. The printf() function will be called just once, after the loop has been completed.

In fragment 2, the braces ensure that both statements are part of the while loop, and printf() is called each time the loop is executed. The entire compound statement is considered to be the single statement in terms of the structure of a while statement (see Figure 5.7).

![](bbox=[0.21, 0.55, 0.78, 0.81])

Figure 5.7 A while loop with a compound statement.