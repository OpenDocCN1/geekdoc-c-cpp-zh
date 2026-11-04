```
```text
// Zero placeholders
// Inserts zeros if no digit appears at the given position
Console.WriteLine(i.ToString("00000", enUS)); // 01234

// Decimal point
// Here mixed used with trailing zero padding
Console.WriteLine(d.ToString("0###.##", enUS)); // 0123.46
```
```

Other custom specifiers are available, whose documentation can be found on MSDN. Some of them are very powerful, but as a result sometimes have rather cryptic syntax.

# MINI LANGUAGES

Unfortunately, format strings are one of those leftover mini-languages that tend to invade frameworks. An unfortunate implication of this is the need for developers to learn them separately from the programming languages being used. Also, the language doesn’t care about those opaque strings and doesn’t perform any kind of compile-time checking for them.

It has been a good trend to eliminate such magic strings; for example, by language features such as LINQ (instead of using, say, T-SQL) and even C# 4.0 dynamic (instead of specifying, say, a method as a string). First-class math specifiers would likely be quite complicated but could work.

Until further notice, format strings are a necessary evil that can result in signaling of runtime errors if unsupported specifiers are used, or when they’re used in an improper fashion (for example, use of D on a fractional number).

Formatting doesn’t only apply to numbers. Lots of other types have a formatting story as well. A few examples are shown here:

```
```text
// Date patterns without time
// Others include date/time, UTC, year/month, roundtrip, etc.
var bd = new DateTime(1983, 2, 11);
Console.WriteLine(bd.ToString("d", nlBE)); // 11/02/1983
Console.WriteLine(bd.ToString("D", nlBE)); // vrijdag 11 februari 1983

// Custom date/time specifiers
// ddd = short day of week; dd = day of month; MM = month
Console.WriteLine(bd.ToString("ddd dd/MM", enUS)); // Fri 11/02
```
```

There’s no use in cloning the MSDN documentation here. What matters most is to have gotten some familiarity with the richness of formatting, enough to encourage you to explore format strings in more detail.