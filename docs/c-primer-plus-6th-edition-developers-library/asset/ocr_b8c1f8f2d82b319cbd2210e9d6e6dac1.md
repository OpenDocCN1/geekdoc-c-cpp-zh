You could have controlled the loop this way:

```
while (scanf("%f %f", &length, &width) == 2)
```

However, using break makes it simple to echo each input value individually.

As with continue, don’t use break when it complicates code. For example, consider the following loop:

```
while ((ch = getchar()) != '\n')
{
    if (ch == '\t')
        break;
    putchar(ch);
}
```

The logic is clearer if both tests are in the same place:

```
while ((ch = getchar()) != '\n' && ch != '\t')
    putchar(ch);
```

The break statement is an essential adjunct to the switch statement, which is coming up next.

A break statement takes execution directly to the first statement following the loop; unlike the case for continue in a for loop, the update part of the control section is skipped. A break in a nested loop just takes the program out of the inner loop; to get out of the outer loop requires a second break:

```
int p, q;

scanf("%d", &p);
while ( p > 0 )
{
    printf("%d\n", p);
    scanf("%d", &q);
    while( q > 0 )
    {
        printf("%d\n",p*q);
        if (q > 100)
            break;        // break from inner loop
        scanf("%d", &q);
    }
    if (q > 100)
        break;            // break from outer loop
    scanf("%d", &p);
}
```