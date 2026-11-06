```
```cpp
do
{
    cout << i << endl;
    i++;
}
while (i <= 5);
cout << "All Finished!" << endl;
return 0;
}
```
```

Notice here that the loop starts with the do keyword, and then the material for the loop follows inside braces, and finally the while statement appears at the end. The idea is that you’re telling the computer “Do this while such-and-such is true,” where this is the stuff inside braces and the such-and-such is the condition inside the parentheses. Because the condition is evaluated at the end, after everything else is done, the output from this example is a little different from the other while loop examples:

```
```text
15
All Finished!
```
```

![](bbox=[0.173, 0.473, 0.239, 0.539])

If you had used a while loop here, the loop wouldn’t have executed at all because i is set to 15. However, because this is a do-while loop, you see the output of 15. Having the loop run at least once can be a problem sometimes, and if you don’t want that behavior, consider using a while loop instead of a do-while loop.

# Breaking and continuing

Sometimes, you may write an application that includes a loop that does more than simply add numbers. You may find that you want the loop to end under a condition that’s separate from the condition in the loop declaration. Or you may want the loop to suddenly skip out of the current loop and continue with the next item in the loop when the item being processed is incorrect in some way. When you stop a loop and continue with the code after the loop, you use a break statement. When you quit the current cycle of the loop and continue with the next cycle, you use a continue statement. The next two sections show you how to do this.

![](bbox=[0.174, 0.796, 0.239, 0.862])

Even though the examples in the following sections rely on a for loop, the break and continue statements also work for while and do-while loops.