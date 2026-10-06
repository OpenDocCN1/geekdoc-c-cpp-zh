# Chapter 7: Chaining and Interaction 187

Figure 7-3 shows an animation of a sailing ship that slowly fades into view and sails across the browser, then fades out again. Before each trip the global variable KEY_PRESS is checked and the animation repeats until the space bar is pressed.

# About the Plug-in

This plug takes an expression and an array of statements to chain if the expression evaluates to true. It requires the following parameters:

+   * expr A string containing an expression that can be evaluated to true or false
* calls An array of strings containing a sequence of plug-ins to place in the chain

# Variables, Arrays, and Functions

| | |
|---|---|
| temp | Local string variable used for reconstructing a string from the array in calls |
| j | Local variable for iterating through the calls array |
| eval() | Function to evaluate a JavaScript expression |
| replace() | Function to replace parts of a string |
| substr() | Function to return part of a string |
| push() | Function to push a value onto an array |
| InsVars() | Plug-in for inserting values into a string |
| Chain() | Plug-in for chaining sequences of plug-ins together |

# How It Works

This plug-resides within an if statement and completes only if the string passed in expr evaluates to true, like this:

```
if (eval(expr))
```

![](bbox=[0.129, 0.686, 0.839, 0.921])