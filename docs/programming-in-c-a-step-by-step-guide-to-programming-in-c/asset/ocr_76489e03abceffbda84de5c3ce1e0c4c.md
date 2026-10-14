# ## 4.9 The *break* statement and continue statement

The purpose of *break* statement is to break out of a loop (**while, do while, or for loop**) or a switch statement. When a **break** statement is encountered inside a loop, the loop is immediately exited and the program continues with the statement immediately following the loop. When the loops are nested, the **break** would only exit from the loop containing it. That is, the **break** would exit only a single loop.

**Syntax**: `break;`

**Program 4.9: Program to illustrate the use of *break* statement.**

```
```c
void main()
{
    int x;
    for(x=1; x<=10; x++)
    {
        if(x==5)
            break; /* break loop only if x == 5 */
        printf("%d", x);
    }
    printf("\nBroke out of loop");
}
```
```