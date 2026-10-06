The message module displays the string "This is a recursive module." and then calls itself. Each time it calls itself, the cycle is repeated. Can you see a problem with the module? There's no way to stop the recursive calls. This module is like an infinite loop because there is no code to stop it from repeating.

Like a loop, a recursive module must have some way to control the number of times it repeats. The pseudocode in Program 13-2 shows a modified version of the message module. In this program, the message module receives an Integer that specifies the number of times the module should display the message.

# Program 13-2

```
Module main()
  // By passing the argument 5 to the message module,
  // we are telling it to display the message
  // five times.
  Call message(5)
End Module

Module message(Integer times)
  If times > 0
    Display "This is a recursive module.
    Call message(times - 1)
  End If
End Module
```

# Program Output

This is a recursive module.
This is a recursive module.
This is a recursive module.
This is a recursive module.
This is a recursive module.

The message module in this program contains an If-Then statement (in lines 9 through 12) that controls the recursion. As long as the times parameter is greater than zero, the message "This is a recursive module." is displayed, and then the module calls itself again. Each time it calls itself, it passes times - 1 as the argument.

The main module calls the message module passing the argument 5. The first time the module is called, the If-Then statement displays the message and then calls itself with 4 as the argument. Figure 13-1 illustrates this.

# Figure 13-1 First two calls of the module

![](bbox=[0.345, 0.808, 0.625, 0.938])