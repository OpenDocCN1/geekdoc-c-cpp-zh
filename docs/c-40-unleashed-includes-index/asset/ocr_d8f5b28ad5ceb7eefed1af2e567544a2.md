![](bbox=[0.08, 0.14, 0.6, 0.62])

FIGURE 7.21 Generated code for an iterator.

All we have to do now is patch up our consuming code:

```
foreach (int prime in GetPrimes(int.MaxValue))
{
    Console.WriteLine(prime);

    Console.Write("Want More? ");
    if (!Console.ReadLine().ToLower().StartsWith('y'))
        break;
}
```

The most important property of an iterator is without doubt the fact it keeps the code readable, as it was intended to look in the first place. Everyone knows return; now you simply use yield return and don’t have to worry with all the bookkeeping around suspending and resuming the iterator’s execution. All such plumbing is taken care of by the compiler.

![](bbox=[0.03, 0.88, 0.08, 0.95])

To whet your appetite about LINQ, let’s give away the implementation of one of its query operators: Where (a method, hence with a capital letter). We’ve already used the where clause (a keyword, hence a lowercase letter) in a previous example to filter out those processes whose memory footprint is larger than 50MB: