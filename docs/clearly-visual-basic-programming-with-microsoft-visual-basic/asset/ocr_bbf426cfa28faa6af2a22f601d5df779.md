You make a control blink using code that changes the control’s Visible property while the application is running. The way the property is changed depends on its initial setting. If the Visible property is set to True in the Properties window, the code will need to set the property to False and then back to True for each blink. On the other hand, if the Visible property’s initial setting is False, the code must switch the property to True and then back to False for each blink. In the My Dream Car-Version 1 application, the lblMessage control’s Visible property is set to False in the Properties window. Therefore, to make the control blink once, the code will need to set the Visible property twice: first to True and then to False. Similarly, to make the control blink twice, the code needs to set the Visible property four times: first to True, then to False, then to True, and finally to False. The Click Me button’s Click event procedure will make the control blink 10 times, so it will need to set the Visible property 20 times, alternating between the True and False settings. You will use a counter variable to keep track of the number of times the Visible property is set.

Switching the Visible property isn’t all that is necessary to make a control blink. Because the computer will process the switching instructions so rapidly, you won’t even notice that the control is blinking. To actually see the control blink, you will need to both refresh the interface and delay program execution each time you change the Visible property’s setting. You refresh the interface using the form’s Refresh method. The **Refresh method** will ensure that any code appearing before it that affects the interface’s appearance is processed. The Refresh method’s syntax is **Me.Refresh()**, where Me refers to the current form. You can delay program execution using the **Sleep method** in the following syntax: **System.Threading.Thread.Sleep(** *milliseconds* **)**. The *milliseconds* argument is the number of milliseconds to suspend the program. A millisecond is 1/1000 of a second; in other words, there are 1000 milliseconds in a second. Figure 13-9 shows the algorithm for the Click Me button’s Click event procedure.

```
```
1. assign 1 to a counter variable
2. repeat while the counter variable’s value is less than or equal to 20:
    if the lblMessage control’s Visible property is set to True
        set the property to False
    else
        set the property to True
    end if
    refresh the interface
    delay program execution for 1/4 second
    add 1 to the counter variable
end repeat
```
```

Figure 13-9: Algorithm for the Click Me button’s Click event procedure in Version 1