# 19.2. Code Review - Roman Numeral Converter

roman-numerals/SNumeral.cs (lines 26-47)

```
```
    internal static void Main() {
        var r1 = new SNumeral(1234);
        Console.WriteLine($"r1 = {r1}");

        var r2 = new SNumeral(2022);
        Console.WriteLine($"r2 = {r2}");

        var r3 = new SNumeral("MMXXII");
        Console.WriteLine($"r3 = {r3}\n");

        Console.WriteLine($"{r1 == r2 ? "r1 = r2" : "r1 != r2"}");
        Console.WriteLine($"{r2 == r3 ? "r2 = r3" : "r2 != r3"}");
    }
```
```

The following is a definition of CNumeral (C for class). The CNumeral type is defined as a class.