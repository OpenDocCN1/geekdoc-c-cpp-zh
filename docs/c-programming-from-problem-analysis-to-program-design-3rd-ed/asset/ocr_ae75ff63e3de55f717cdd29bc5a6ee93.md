```
```csharp
static void Main()
{
    string inputStringValue;
    double aValue;
    double result;

    Console.Write("Enter a value to be " + "squared: ");
    inputStringValue = Console.ReadLine();
    aValue = double.Parse(inputStringValue);
    result = Math.Pow(aValue, 2);
    Console.WriteLine("{0} squared is {1}", aValue, result);
}
```
```

Calls to methods char.Parse( ) and bool.Parse( ) produce similar results, as shown in Example 3-11.

# Example 3-11

```
```csharp
string sValue = "True";
Console.WriteLine(bool.Parse(sValue));    // displays True
string strValue = "q";
Console.WriteLine(char.Parse(strValue));    // displays q
```
```

If you attempt to parse an incompatible value, a System.FormatException error, similar to that shown in Figure 3-6, is generated. The error in Figure 3-6 was generated from Console.WriteLine(char.Parse(sValue)) when sValue referenced "True", as in Example 3-11.

![](bbox=[0.17, 0.82, 0.77, 0.91])

# Figure 3-6 System.FormatException run-time error