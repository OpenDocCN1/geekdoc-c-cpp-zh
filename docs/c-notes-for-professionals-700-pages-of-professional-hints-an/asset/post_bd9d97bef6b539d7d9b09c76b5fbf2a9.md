
You can also arbitrarily create tuples in code:

```
var name = ("John", "Smith");
Console.WriteLine(name.Item1);
// Outputs John

Console.WriteLine(name.Item2);
// Outputs Smith
```

When creating a tuple, you can assign ad-hoc item names to the members of the tuple:

```
var name = (first: "John", middle: "Q", last: "Smith");
Console.WriteLine(name.first);
// Outputs John
```

## Type inference

Multiple tuples defined with the same signature (matching types and count) will be inferred as matching types. For example:

```
public (int sum, double average) Measure(List<int> items)
{
    var stats = (sum: 0, average: 0d);
    stats.sum = items.Sum();
    stats.average = items.Average();
    return stats;
}
```

stats can be returned since the declaration of the stats variable and the method's return signature are a match.

## Reflection and Tuple Field Names

Member names do not exist at runtime. Reflection will consider tuples with the same number and types of members the same even if member names do not match. Converting a tuple to an object and then to a tuple with the same member types, but different names, will not cause an exception either.

While the ValueTuple class itself does not preserve information for member names the information is available through reflection in a TupleElementNamesAttribute. This attribute is not applied to the tuple itself but to method parameters, return values, properties and fields. This allows tuple item names to be preserved across assemblies i.e. if a method returns (string name, int count) the names name and count will be available to callers of the method in another assembly because the return value will be marked with TupleElementNamesAttribute containing the values "name" and "count".

## Use with generics and async

The new tuple features (using the underlying ValueTuple type) fully support generics and can be used as generic type parameter. That makes it possible to use them with the async/await pattern:

```
public async Task<(string value, int count)> GetValueAsync()
{
    string fooBar = await _stackoverflow.GetStringAsync();
    int num = await _stackoverflow.GetIntAsync();
    return (fooBar, num);
}
```

## Use with collections

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

## Differences between ValueTuple and Tuple

The primary reason for introduction of ValueTuple is performance.

| Type name | ValueTuple | Tuple |
|---|---|---|
| Class or structure | struct | class |
| Mutability (changing values after creation) | mutable | immutable |
| Naming members and other language support | yes | no (TBD) |

## References

- Original Tuples language feature proposal on GitHub
- A runnable VS 15 solution for C# 7.0 features
- NuGet Tuple Package

## Section 71.2: Local functions

Local functions are defined within a method and aren’t available outside of it. They have access to all local variables and support iterators, async/await and lambda syntax. This way, repetitions specific to a function can be functionalized without crowding the class. As a side effect, this improves intellisense suggestion performance.

### Example

```
double GetCylinderVolume(double radius, double height)
{
    return getVolume();

    double getVolume()
    {
        // You can declare inner-local functions in a local function
        double GetCircleArea(double r) => Math.PI * r * r;

        // ALL parents' variables are accessible even though parent doesn't have any input.
        return GetCircleArea(radius) * height;
    }
}
```

Local functions considerably simplify code for LINQ operators, where you usually have to separate argument checks from actual logic to make argument checks instant, not delayed until after iteration started.

### Example

```
public static IEnumerable<TSource> Where<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate)
{
    if (source == null) throw new ArgumentNullException(nameof(source));
    if (predicate == null) throw new ArgumentNullException(nameof(predicate));

    return iterator();

    IEnumerable<TSource> iterator()
    {
        foreach (TSource element in source)
            if (predicate(element))
                yield return element;
    }
}
```

Local functions also support the async and await keywords.

### Example

```
async Task WriteEmailsAsync()
{
    var emailRegex = new Regex("@(\?i)[a-z0-9-_.+]+@[a-z0-9-]+\.[a-z0-9-.]+" );
    IEnumerable<string> emails1 = await getEmailsFromFileAsync("input1.txt");
    IEnumerable<string> emails2 = await getEmailsFromFileAsync("input2.txt");
    await writeLinesToFileAsync(emails1.Concat(emails2), "output.txt");
```

```csharp
async Task<IEnumerable<string>> getEmailsFromFileAsync(string fileName)
{
    string text;

    using (StreamReader reader = File.OpenText(fileName))
    {
        text = await reader.ReadToEndAsync();
    }

    return from Match emailMatch in emailRegex.Matches(text) select emailMatch.Value;
}

async Task writeLinesToFileAsync(IEnumerable<string> lines, string fileName)
{
    using (StreamWriter writer = File.CreateText(fileName))
    {
        foreach (string line in lines)
        {
            await writer.WriteLineAsync(line);
        }
    }
}
```

One important thing that you may have noticed is that local functions can be defined under the `return` statement, they do **not** need to be defined above it. Additionally, local functions typically follow the "lowerCamelCase" naming convention as to more easily differentiate themselves from class scope functions.

## Section 71.3: out var declaration

A common pattern in C# is using `bool TryParse(object input, out object value)` to safely parse objects.

The `out var` declaration is a simple feature to improve readability. It allows a variable to be declared at the same time that it is passed as an out parameter.

A variable declared this way is scoped to the remainder of the body at the point in which it is declared.

### Example

Using TryParse prior to C# 7.0, you must declare a variable to receive the value before calling the function:

```
```csharp
Version < 7.0
int value;
if (int.TryParse(input, out value))
{
    Foo(value); // ok
}
else
{
    Foo(value); // value is zero
}

Foo(value); // ok
```
```

In C# 7.0, you can inline the declaration of the variable passed to the `out` parameter, eliminating the need for a separate variable declaration:

```
```csharp
Version ≥ 7.0
if (int.TryParse(input, out var value))
```
```
