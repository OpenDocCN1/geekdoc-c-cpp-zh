```
void payCheck_Click(object sender, EventArgs e)
{
    // This code will execute when the button is clicked.
}
```

As you might expect, to remove an event handler from an event, the dual -= syntax is used.

In the context of UI development, those event handlers are set up by code emitted through the UI designer tools. Events are useful in other contexts too, though, where a pure code-driven approach will be required to hook up the handlers.

# A Gentle Introduction to Definite Assignment

A significant part of the language specification deals with rules of definite assignment, in short to ensure a variable is not used before it has been assigned to. Use of unassigned variables has been a historical source of many bugs, and C# wants to avoid these kinds of mishaps.

Let's set the scene by looking at some simple native C/C++ code. What will the following code print to the screen?

```
void main()
{
    int x;
    printf("%d\n", x);
}
```

Before answering, notice the code will compile fine. In fact, some C/C++ compilers (for example, Microsoft's) will raise a red flag by emitting a warning:

```
warning C4700: uninitialized local variable 'x' used
```

But warnings can be ignored. As you will see, in C# this code would not compile because the language treats this condition as an error instead. You can see why from the result of executing the preceding C/C++ code, as shown in Figure 5.26.

![](bbox=[0.08, 0.78, 0.5, 0.96])

FIGURE 5.26 An uninitialized variable exposing garbage.