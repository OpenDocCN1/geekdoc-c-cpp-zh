# Chapter 15: String Interpolation

# Section 15.1: Format dates in strings

```
```csharp
var date = new DateTime(2015, 11, 11);
var str = $"It's {date:MMMM d, yyyy}, make a wish!";
System.Console.WriteLine(str);
```
```

You can also use the DateTime.ToString method to format the DateTime object. This will produce the same output as the code above.

```
```csharp
var date = new DateTime(2015, 11, 11);
var str = date.ToString("MMMM d, yyyy");
str = "It's " + str + ", make a wish!";
Console.WriteLine(str);
```
```

# Output:

It's November 11, 2015, make a wish!

Live Demo on .NET Fiddle

Live Demo using DateTime.ToString

> Note: MM stands for months and mm for minutes. Be very careful when using these as mistakes can introduce bugs that may be difficult to discover.

# Section 15.2: Padding the output

String can be formatted to accept a padding parameter that will specify how many character positions the inserted string will use :

```
```
${value, padding}
```
```