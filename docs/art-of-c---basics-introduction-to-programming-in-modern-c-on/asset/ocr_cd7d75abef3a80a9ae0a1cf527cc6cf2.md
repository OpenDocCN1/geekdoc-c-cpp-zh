# *roman-numerals/RcNumeral.cs*

```

namespace Roman;

public sealed record RcNumeral() {
    private readonly ushort number;

    public RcNumeral(string repr): this() =>
        number = NumeralHelper.Validate(repr) ?
        NumeralHelper.FromNumeralString(repr) :
            throw new ArgumentException($"Invalid Roman numeral:
            {repr}");

    public ushort Number {
        get => number;
        init => number = value switch {
            >= Constants.MIN and <= Constants.MAX => value,
            _ => throw new ArgumentOutOfRangeException($"Roman numerals
            are between {Constants.MIN} and {Constants.MAX}"),
        };
    }

    public string Roman => NumeralHelper.ToNumeralString(number);

    internal static void Main() {
        var r1 = new RcNumeral { Number = 1234 };
        Console.WriteLine($"r1 = {r1}");

        var r2 = new RcNumeral() { Number = 2022 };
        Console.WriteLine($"r2 = {r2}");

        var r3 = new RcNumeral("MMXXII");
        Console.WriteLine($"r3 = {r3}\n");

        Console.WriteLine($"{(r1 == r2 ? "r1 == r2" : "r1 != r2")}");
        Console.WriteLine($"{(r2 == r3 ? "r2 == r3" : "r2 != r3")}");
    }
}

```