For example, you may have some code like this:

```
```cpp
total = 10;
for (i = 0; i < 10; i++)
{
    total = (total + i) * 3;
}
```
```

But this code may not be clear to your coworkers (or to you, if you put it away for six months and come back later to look at it). So instead, you can add some comments. You denote a comment in C++ by starting a line with two slashes, like this:

```
```cpp
// Initialize total to the number
// of items involved.
total = 10;

// Calculate total for the
// first ten sets
for (i = 0; i < 10; i++)
{
    total = (total + i) * 3;
}
```
```

Now the people working on the project can understand what the code does. Note the white space between the groups of code. Using white space helps someone looking at the code see where one “thought” ends and another begins. You should always include white space in your code so that other developers can read the code more easily.

Of course, you could put comments like this:

```
```cpp
// My salary is too low
// I want a raise
total = 10;

// Someday they'll recognize
// my superior talents!
for (i = 0; i < 10; i++)
{
    total = (total + i) * 3;
}
```
```

However, comments like this don’t have much use in the code; besides, they may have the reverse effect from the one you’re hoping for!

![](bbox=[0.143, 0.787, 0.229, 0.861])

A comment is ignored by a compiler (but not always by other humans). You can write whatever you want as comments, and the compiler pretends that it’s not even there. (Your boss, however, may notice, so use discretion.)

![](bbox=[0.152, 0.866, 0.231, 0.939])

A comment begins with //, and it can begin anywhere on the line. In fact, contrary to what you might think, you can even put comments at the end of a line containing C++ code, instead of on a separate line. Using comments on a code line lets you focus a comment on just that line, as follows:

```
```cpp
int subtotal = 10;  // Initialize the subtotal value to 10.
```
```