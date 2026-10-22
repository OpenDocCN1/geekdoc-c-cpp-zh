```
int imin(int n,int m)
{
    int min;

    if (n < m)
        min = n;
    else
        min = m;

    return min;
}
```

Recall that scanf() returns the number of items successfully read, so input other than two integers will cause the while loop to terminate. Here is a sample run:

```
Enter a pair of integers (q to quit):
509 333
The lesser of 509 and 333 is 333.
Enter a pair of integers (q to quit):
-9393 6
The lesser of -9393 and 6 is -9393.
Enter a pair of integers (q to quit):
q
Bye.
```

The keyword return causes the value of the following expression to be the return value of the function. In this case, the function returns the value that was assigned to min. Because min is type int, so is the imin() function.

The variable min is private to imin(), but the value of min is communicated back to the calling function with return. The effect of a statement such as the next one is to assign the value of min to lesser:

```
lesser = imin(n,m);
```

Could you say the following instead?

```
imin(n,m);
lesser = min;
```

No, because the calling function doesn’t even know that min exists. Remember that imin()’s variables are local to imin(). The function call imin(evil1,evil2) copies the values of one set of variables to another set.

Not only can the returned value be assigned to a variable, it can also be used as part of an expression. You can do this, for example:

```
answer = 2 * imin(z, zstar) + 25;
printf("%d\n", imin(-32 + answer, LIMIT));
```