Ignore the use of the string formatter for now. Intuitively, you should be able to see what {0} and {1} stand for.

Break and continue statements are available for for loops just as they are for other kinds of loops. The following is an example of the use of a break statement in the context of a for loop:

```
static void PrintPrimes(int max)
{
    for (int num = 2; num < max; num++)
    {
        bool foundDiv = false;

        for (int div = 2; div <= Math.Sqrt(num); div++)
        {
            if (num % div == 0)
            {
                foundDiv = true;
                break;
            }
        }

        if (!foundDiv)
        {
            Console.WriteLine(num);
        }
    }
}
```

Be aware that this algorithm for finding prime numbers is not the most intelligent one and is meant only to illustrate nested loops and the use of the break statement. Notice that in the condition for the inner for statement a comparison is done between an integer value and a floating-point number resulting from the Math.Sqrt call. This works because an implicit conversion from int to double is available.

Finally, although some people prefer while (true) as the most appropriate way to write an infinite loop, others believe they can make more of a statement using an obscure for loop. I disagree with the latter group but leave the judgment to you (you agree!):

```
for (;;)
{
    // Do something for"ever"; the (;;) above doesn't really read like "ever".
}
```