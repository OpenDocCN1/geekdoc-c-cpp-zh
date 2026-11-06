# Table 1 while Loop Examples

| Loop | Output | Explanation |
|---|---|---|
| `i = 5;`<br>`while (i > 0)`<br>`{`<br>`    cout << i << " ";`<br>`    i--;`<br>`}` | `5 4 3 2 1` | When `i` is 0, the loop condition is false, and the loop ends. |
| `i = 5;`<br>`while (i > 0)`<br>`{`<br>`    cout << i << " ";`<br>`    i++;`<br>`}` | `5 6 7 8 9 10 11 ...` | The `i++` statement is an error causing an "infinite loop" (see Common Error 4.1 on page 136). |
| `i = 5;`<br>`while (i > 5)`<br>`{`<br>`    cout << i << " ";`<br>`    i--;`<br>`}` | `(No output)` | The statement `i > 5` is false, and the loop is never executed. |
| `i = 5;`<br>`while (i < 0)`<br>`{`<br>`    cout << i << " ";`<br>`    i--;`<br>`}` | `(No output)` | The programmer probably thought, "Stop when `i` is less than 0". However, the loop condition controls when the loop is executed, not when it ends (see Common Error 4.2 on page 137). |
| `i = 5;`<br>`while (i > 0) ;`<br>`{`<br>`    cout << i << " ";`<br>`    i--;`<br>`}` | `(No output, program does not terminate)` | Note the semicolon before the `{`. This loop has an empty body. It runs forever, checking whether `i > 0` and doing nothing in the body. |

# Common Error 4.1

![](bbox=[0.152, 0.766, 0.22, 0.818])

# Infinite Loops

A very annoying loop error is an *infinite loop*: a loop that runs forever and can be stopped only by killing the program or restarting the computer. If there are output statements in the program, then line after line of output flashes by on the screen. Otherwise, the program just sits there and hangs, seeming to do nothing. On some systems, you can terminate a hanging program by hitting Ctrl + C. On others, you can close the window in which the program runs.

A common reason for infinite loops is forgetting to update the variable that controls the loop:

```
~~~cpp
year = 1;
while (year <= 20)
{
~~~
```