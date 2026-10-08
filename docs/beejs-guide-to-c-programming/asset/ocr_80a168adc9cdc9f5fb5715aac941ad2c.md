# Chapter 4

# Functions

"Sir, not in an environment such as this. That's why I've also been programmed for over thirty secondary functions that—"

—C3PO, before being rudely interrupted, reporting a now-impressive number of additional functions, Star Wars script

Very much like other languages you're used to, C has the concept of functions.

Functions can accept a variety of arguments and return a value. One important thing, though: the arguments and return types are predeclared—that's how C calls it!

Let's take a look at this function. This is a function that takes an int as an argument, and returns an int.

```
#include <stdio.h>

int plus_one(int n) // The "definition"
{
    return n + 1;
}
```

The int before the plus_one indicates the return type.
The int indicates that this function takes int argument, stored in parameter n. A parameter is a special type of local variable into which arguments are copied.

I'm going to drive home the point that the arguments are copied into the parameters, here. Lots of things in C are easier to understand if you know that the parameter is a copy of the argument, not the argument itself. More on that in a minute.

Continuing the program down into main(), we can see the call to the function, where we assign the return value into local variable j:

```
int main(void)
{
    int i = 10, j;

    j = plus_one(i); // The "call"

    printf("%i + 1 is %d\n", j);
}
```