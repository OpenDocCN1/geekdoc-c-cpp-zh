# *roman-numerals/CNumeral.cs*

```
```
namespace Roman;
public sealed class CNumeral {
    private readonly ushort number;
    public CNumeral(long number = 1) => this.number = number switch {
        >= Constants.MIN and <= Constants.MAX => (ushort)number,
        _ => throw new ArgumentOutOfRangeException($"Roman numerals are
between {Constants.MIN} and {Constants.MAX}"),
    };
    public CNumeral(string repr) : this(
        NumeralHelper.Validate(repr) ?
        NumeralHelper.FromNumeralString(repr) :
            throw new ArgumentException($"Invalid Roman numeral:
{repr}")) { }
    public override string ToString() =>
        NumeralHelper.ToNumeralString(number);
    internal static void Main() {
        var r1 = new CNumeral(1234);
        Console.WriteLine($"r1 = {r1}");
        var r2 = new CNumeral(2022);
        Console.WriteLine($"r2 = {r2}");
        var r3 = new CNumeral("MMXXII");
        Console.WriteLine($"r3 = {r3}\n");
        Console.WriteLine($"{(r1 == r2 ? "r1 == r2" : "r1 != r2")}");
        Console.WriteLine($"{(r2 == r3 ? "r2 == r3" : "r2 != r3")}");
    }
}
```
```

# *roman-numerals/SNumeral.cs*

600