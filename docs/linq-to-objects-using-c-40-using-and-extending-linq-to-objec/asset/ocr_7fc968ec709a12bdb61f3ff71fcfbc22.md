# WRITING A SINGLE ELEMENT OPERATOR

```
// the Count() extension method already has this
// optimization built-in. I'm showing it here to
// make the-point it is being considered!
int count = 0;
if (source is ICollection)
    count = ((ICollection)source).Count;
else
    count = source.Count();
```

```
if (count == 0)
    throw new InvalidOperationException("No elements");
```

```
// use the passed in seed value, or use time-based
Random random;
if (seed == 0)
    random = new Random();
else
    random = new Random(seed);
```

```
// IList implementers, access by indexer. It's faster.
IList<T> list = source as IList<T>;
if (list != null)
{
    int index = random.Next(0, count);
    return list[index];
}
```

```
else
{
    // Other collection types must be
    // enumerated (eg. Dictionary, IEnumerable)
    int index = random.Next(0, count);
    using (IEnumerator<T> e = source.GetEnumerator())
    {
        // move to the first element (the initial
        // position is BEFORE the first element.
        e.MoveNext();
```

```
// iterate and move until we hit our index
while (index > 0)
    {
        e.MoveNext();
        index--;
    }
```