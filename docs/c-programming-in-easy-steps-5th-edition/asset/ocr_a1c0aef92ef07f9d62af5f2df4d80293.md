![](bbox=[0.229, 0.071, 0.771, 0.173])

This unsatisfactory result shows that **cin** reads up to the first space, leaving the second name in the input buffer, which is then read by **getline()** and subsequently output. The problem persists even when you enter only your first name, because **cin** leaves the newline character, created when you hit Return, on the input buffer.

+   6. Edit the program to resolve this issue by inserting a statement, just before the call to the **getline** function, instructing it to ignore content in the input buffer.

```
```cpp
cin.ignore(256, '\n');
```
```

+   7. Save, compile, and run the program again, then re-enter your full name to see the program perform as required.

![](bbox=[0.256, 0.335, 0.745, 0.436])

![](bbox=[0.118, 0.449, 0.209, 0.506])

Use the **cin** function for numeric input or single word input, but use the **getline()** function for string input.

![](bbox=[0.118, 0.555, 0.209, 0.613])

The arguments to the **cin.ignore()** function specify it should discard up to 256 characters and stop when it encounters a newline character.