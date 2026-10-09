# roman-numerals/CNumeral.cs (lines 3-15)

```
public sealed class CNumeral {
    private readonly ushort number;

    public CNumeral(long number = 1) => this.number = number switch {
        >= Constants.MIN and <= Constants.MAX => (ushort)number,
        _ => throw new ArgumentOutOfRangeException($"Roman numerals
    are between {Constants.MIN} and {Constants.MAX}"),
    };

    public CNumeral(string repr) : this(
        NumeralHelper.Validate(repr) ?
    NumeralHelper.FromNumeralString(repr) :
        throw new ArgumentException($"Invalid Roman numeral: 
    {repr}")) { }

    public override string ToString() =>
        NumeralHelper.ToNumeralString(number);
}
```

Here are two other definitions of Roman number, RcNumeral (rc for record class) and RsNumeral (rs for record struct). The RcNumeral and RsNumeral types are defined as class and struct, respectively, with the record keyword.