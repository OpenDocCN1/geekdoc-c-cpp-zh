# 3.10. FUNCTIONS WITH MULTIPLE PARAMETERS

stack diagrams show the value of each variable, but the variables are contained in larger boxes that indicate which function belong to. For example, the state diagram for printTwice looks like this:

![](bbox=[0.296, 0.291, 0.7, 0.483])

Whenever a function is called, it creates a new instance of that function. Each instance of a function contains the parameters and local variables for that function. In the diagram an instance of a function is represented by a box with the name of the function on the outside and the variables and inside. In the example, main has one local variable, argument, and no parameters. printTwice has no local variables and one parameter, named phil.

# 3.10 Functions with multiple parameters

The syntax for declaring and invoking functions with multiple parameters is a common source of errors. First, remember that you have to declare the type of every parameter. For example

```
void printTime(int hour, int minute) {
    cout << hour;
    cout << ":";
    cout << minute;
}
```

It might be tempting to write (int hour, minute), but that format is only legal for variable declarations, not for parameters. Another common source of confusion is that you do not have to declare the type of arguments. The following is wrong!

```
int hour = 11;
int minute = 59;
printTime(int hour, int minute); // WRONG!
```