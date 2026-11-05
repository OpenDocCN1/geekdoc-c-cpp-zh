It may become beneficial to have a collection of tuples in (as an example) a scenario where you're attempting to find a matching tuple based on conditions to avoid code branching.

Example:

```
private readonly List<Tuple<string, string, string>> labels = new List<Tuple<string, string, string>>()
{
    new Tuple<string, string, string>("test1", "test2", "Value"),
    new Tuple<string, string, string>("test1", "test1", "Value2"),
    new Tuple<string, string, string>("test2", "test2", "Value3"),
};

public string FindMatchingValue(string firstElement, string secondElement)
{
    var result = labels
        .Where(w => w.Item1 == firstElement && w.Item2 == secondElement)
        .FirstOrDefault();

    if (result == null)
        throw new ArgumentException("combo not found");

    return result.Item3;
}
```

With the new tuples can become:

```
private readonly List<(string firstThingy, string secondThingyLabel, string foundValue)> labels = new List<(string firstThingy, string secondThingyLabel, string foundValue)>()
{
    ("test1", "test2", "Value"),
    ("test1", "test1", "Value2"),
    ("test2", "test2", "Value3"),
}

public string FindMatchingValue(string firstElement, string secondElement)
{
    var result = labels
        .Where(w => w.firstThingy == firstElement && w.secondThingyLabel == secondElement)
        .FirstOrDefault();

    if (result == null)
        throw new ArgumentException("combo not found");

    return result.foundValue;
}
```

Though the naming on the example tuple above is pretty generic, the idea of relevant labels allows for a deeper understanding of what is being attempted in the code over referencing "Item1", "Item2", and "Item3".

# Differences between ValueTuple and Tuple

The primary reason for introduction of ValueTuple is performance.

| Type name | ValueTuple | Tuple |
|---|---|---|
| Class or structure | struct | class |
| Mutability (changing values after creation) | mutable | immutable |
| Naming members and other language support | yes | no (TBD) |