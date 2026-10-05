To avoid such bugs, which can be really hard to find, some recommend always using braces (as well as loops) regardless of whether the statements are one or many.

As we said, if we want to check if some value is true we can write if(i). Some may suggest if(i == true). It is dangerous. For example, see the following code:

```
int i = 20;
if (i == true) // Instead of if(i)
    cout << "One\n";
else
    cout << "Two\n";
```

If i is not bool, as happens in this example, true is converted to the type of i before applying ==. So it is as if we've written if(i == 1), which is not the desired comparison and the code displays Two. In general, no error can easily occur if the comparison is made with a non bool variable.

# THE if-else STATEMENT

As we saw in the previous example, an if statement may have an else clause:

```
if (condition)
{
    ... // block of statements A
}
else
{
    ... // block of statements B
}
```

If the condition is true, the first block of statements is executed; otherwise, the second one. For example:

```
int i = 10, j = -10;
if (i+j)
{
    cout << "One\n";
}
else
{
    cout << "Two\n";
}
```

Since the sum is 0, the condition is false and the code displays Two. Since both blocks consist of a single statement, we could omit the braces and write:

```
if (i+j)
    cout << "One\n";
else
    cout << "Two\n";
```