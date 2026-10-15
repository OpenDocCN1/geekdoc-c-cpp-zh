# SELF-REVIEW QUESTIONS (see answers in Appendix N)

SR 5.17 What is an infinite loop? Specifically, what causes it?

SR 5.18 What output is produced by the following code fragment?

```
int low = 0, high = 10;
while (low < high)
{
    System.out.println (low);
    low++;
}
```

SR 5.19 What output is produced by the following code fragment?

```
int low = 10, high = 0;
while (low <= high)
{
    System.out.println (low);
    low++;
}
```

SR 5.20 What output is produced by the following code fragment?

```
int low = 0, high = 10;
while (low <= high)
{
    System.out.println (low);
    high = high - low;
}
```

SR 5.21 What output is produced by the following code fragment?

```
int low = 0, high = 10, mid;
while (low <= high)
{
    mid = low;
    while (mid <= high)
    {
        System.out.print (mid + " ");
        mid++;
    }
    System.out.println ();
    low++;
}
```

SR 5.22 Assume the int variable value has been initialized to a positive integer. Write a while loop that prints all of the positive divisors of value. For example, if value is 28, it prints divisors of 28: 1 2 4 7 14 28