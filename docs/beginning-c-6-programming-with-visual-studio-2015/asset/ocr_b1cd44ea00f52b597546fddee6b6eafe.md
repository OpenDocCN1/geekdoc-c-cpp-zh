assigned to the variable result will be the int value 11 — the summation of all the elements in the array.

The other two overloads of the Aggregate() extension method are similar, but enable you to perform slightly more complicated processing. This is illustrated in the following short Try It Out.

# TRY IT OUT Using Lambda Expressions with Collections: Ch13Ex09\Program.cs

+   1. Create a new console application called Ch13Ex09 and save it in the directory C:\BegVCSharp\Chapter13.
+   2. Modify the code in Program.cs as follows:
+   3. Run the application. The result is shown in Figure 13-21.

```
```csharp
static void Main(string[] args)
{
    string[] curries = { "pathia", "jalfrezi", "korma" };
    WriteLine(curries.Aggregate(
        (a, b) => a + " " + b));
    WriteLine(curries.Aggregate<string, int>(
        0,
        (a, b) => a + b.Length));
    WriteLine(curries.Aggregate<string, string, string>(
        "Some curries: ",
        (a, b) => a + " " + b,
        a => a));
    WriteLine(curries.Aggregate<string, string, int>(
        "Some curries: ",
        (a, b) => a + " " + b,
        a => a.Length));
    ReadKey();
}
```
```

![](bbox=[0.18, 0.84, 0.65, 0.92])

# How It Works

In this example you experimented with each of the overloads of the Aggregate() extension method, using a string array with three elements as source data.

First, a simple concatenation is performed:

```
```
WriteLine(curries.Aggregate((a, b) => a + " " + b));
```
```