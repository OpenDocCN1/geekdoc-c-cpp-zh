# Inspecting Variable Values

Defining a variable that you want to inspect is referred to as setting a watch for the variable. Before you can set any watches, you must get some variables declared in the program. You can execute the declaration statements by invoking Step Over three times. Use the Step Over menu item, the toolbar icon, or press F10 three times so that the arrow now appears at the start of the line 11:

```
pnumber = &number1;    // Store address in pointer
```

If you look at the Autos window now, it should appear as shown in Figure 10-8 (although the value for &number1 may be different on your system as it represents a memory location). Note that the values for &number1 and pnumber are not equal to each other because the line in which pnumber is set to the address of number1 (the line that the arrow is pointing at) hasn’t yet been executed. You initialized pnumber as a null pointer in the first line of the function, which is why the address it contains is zero. If you had not initialized the pointer, it would contain a junk value-that still could be zero on occasions, of course, because it contains whatever value was left by the last program to use these particular four bytes of memory.

![](bbox=[0.28, 0.38, 0.64, 0.53])

Figure 10-8

The Autos window has five tabs, including the Autos tab that is currently displayed, and the information they show is as follows:

+   The Autos tab shows the automatic variables in use in the current statement and its immediate predecessor (in other words, the statement pointed to by the arrow in the Editor pane and the one before it).

+   The Locals tab shows the values of the variables local to the current function. In general, new variables come into scope as you trace through a program and then go out of scope as you exit the block in which they are defined. In this case, this window always shows values for number1, number2 and pnumber because you have only one function, main(), consisting of a single code block.

+   The Threads tab allows you to inspect and control threads in advanced applications.

+   The Modules tab lists details of the code modules currently executing. If your application crashes, you can determine in which module the crash happened by comparing the address when the crash occurred with the range of addresses in the Address column on this tab.

+   You can add variables to the Watch1 tab that you want to watch. Click a line in the window and type the variable name. You can also watch the value of a C++ expression that you enter in the same way as a variable. You can add up to three additional Watch windows via the Debug > Windows > Watch menu item.