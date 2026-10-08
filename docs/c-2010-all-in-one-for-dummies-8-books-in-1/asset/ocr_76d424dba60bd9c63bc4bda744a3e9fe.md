# Looping Around the Iterator Block 167

The indented line is produced by the nested iteration.

Here are those nested loops in Main() again:

```
MyCollectionIterator mcil = mc.GetEnumerator();
foreach (string s1 in mcil) // Uses the first iterator block
{
    // Do some useful work with each string.
    Console.WriteLine(s1);
    // Find Tony's boss.
    if (s1 == "Tony")
    {
        // In the middle of that iteration, start a new one, using
        // in a second iterator; this is repeated for each other loop pass.
        MyCollectionIterator mcil2 = mc.GetEnumerator();
        foreach (string s2 in mcil2) // Uses the second iterator block
        {
            // Do some useful work with each string.
            if(s2 == "Bob")
            {
                Console.WriteLine(\	(0) is (1)'s boss", s2, s1);
            }
        }
    }
}
```

The original iterator, with MoveNext() and Current, is still more flexible, but this example comes close — and is easier to do.