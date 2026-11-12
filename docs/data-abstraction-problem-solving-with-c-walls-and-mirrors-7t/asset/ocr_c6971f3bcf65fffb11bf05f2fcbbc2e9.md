Strip away the last character
or
Strip away the first character
Consider the first of these alternatives, stripping away the last character, as Figure 2-6 illustrates.

# FIGURE 2-6 A recursive solution

![](bbox=[0.405, 0.255, 0.745, 0.415])

For the solution to be valid, you must write the last character in the string first. Therefore, you must write the last character before you write the remainder of the string backward. A high-level recursive solution, given the string s, is

```
writeBackward(s: string)
if (the string is empty)
    Do nothing--this is the base case
else
{
    Write the last character of s
    writeBackward(s minus its last character)
}
```

> > Note: A recursive solution must involve one or more smaller problems that are each closer to a base case than is the original problem. You must be sure that these smaller problems eventually reach the base case. Failure to do so could result in an algorithm that does not terminate.

This solution to the problem is conceptual. To obtain a C++ function, you must resolve a few implementation issues. Suppose that the function will receive one argument: a string s to be written backward. All characters, including blanks, are part of the string. The C++ function writeBackward appears as follows:

```
/** writes a character string backward.
@pre  The string s to write backward.
@post None.
```