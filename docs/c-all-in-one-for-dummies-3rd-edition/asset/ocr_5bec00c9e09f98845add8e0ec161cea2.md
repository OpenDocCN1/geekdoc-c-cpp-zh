![](bbox=[0.119, 0.134, 0.207, 0.206])

When C++ creates a new variable, it simply creates the variable and doesn’t assign a value to it. The variable contains a junk value — you have no idea of what the variable might contain. This is the reason you never want to use a variable until after you assign a value to it.

+   6. **Click the Next Line button on the Debugger toolbar so that you are one line beyond the following line:**

```
int i = 10;
```

The application changes the value of i to 10, as shown in Figure 3-8. The variable is still shown in red because its value has just changed.

![](bbox=[0.23, 0.334, 0.515, 0.54])

**Figure 3-8:** Assigning a value to *i* changes its value in the Watches window.

+   7. **Click Next Line on the Debugger toolbar.**

The entry for i turns back to show that it has remained stable during the execution of this command. The use of red for changed variables and black for unchanged variables makes it easy to determine which variables have changed.

+   8. **Click Debug/Continue.**

The application ends.

# Watching objects

Objects are just a little bit more complex than variables when you use the Watches window. When you type the name of an object in the Watches window, such as mirror, what you see is the name of the object with a plus sign next to it. Click the plus sign and the view expands to show the content of the object, such as NumberOfPieces, as shown in Figure 3-9.