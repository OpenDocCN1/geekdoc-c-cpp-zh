```
`public delegate int MakeRun();`
```

```
```csharp
/// <summary>
/// The act of consuming all those beverages.
/// </summary>
public class Binge
{
    /// <summary>
    /// What we'll be drinking.
    /// </summary>
    private string beverage;

    /// <summary>
    /// The starting count.
    /// </summary>
    private int count = 0;

    /// <summary>
    /// The manner in which the lyrics are output.
    /// </summary>
    private Writer Sing;

    /// <summary>
    /// What to do when it's all gone.
    /// </summary>
    private MakeRun RiskDUI;

    public event MakeRun OutOfBottles;

    /// <summary>
    /// Initializes the binge.
    /// </summary>
    /// <param name="count">How many we're consuming.</param>
    /// <param name="disasterWaitingToHappen">Our instructions, should we succeed.</param>
```
```
```