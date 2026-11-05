# Table 3-2 Math class methods (continued)

| Method | Description | Method heading |
|---|---|---|
| Log | Returns the logarithm of a specified number. Two overloaded methods. The first one returns the natural (base e) logarithm of a specified number. It takes a single argument of type `double`. The second one (signature to the right) returns the logarithm of a specified number. Example: `Math.Log(4)` returns the value 1.38629436111989 | `public static double Log` `(double, double)` |
| Max | Returns the larger of two specified numbers. Overloaded with 11 different methods (`byte`, `decimal`, `double`, `short`, `int`, `long`, `sbyte`, `float`, `ushort`, `uint`, and `ulong`). All require the same type for both arguments. Example: `Math.Max(87, 13)` returns 87 | `public static double Max` `(double, double)` |
| Min | Returns the smaller of two numbers. Overloaded—exactly like Max in the previous row. Example: `Math.Min(87, 13)` returns 13 | `public static int Min(int, int)` |
| Pow | Returns a specified number raised to the specified power. Not overloaded. Arguments can be entered as `int`. They are implicitly converted. Return value must be stored in `double`; otherwise, you receive a syntax error. Example: `Math.Pow(5, 3)` returns 125 | `public static double Pow` `(double, double)` |