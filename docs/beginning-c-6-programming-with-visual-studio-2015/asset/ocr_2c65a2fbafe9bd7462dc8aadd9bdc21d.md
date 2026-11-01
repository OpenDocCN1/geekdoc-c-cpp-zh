```
```csharp
double? r = GetNullableDouble();
WriteLine($"Input {name} angle (in degrees):");
double? theta = GetNullableDouble();
return new Vector(r, theta);
}
static double? GetNullableDouble()
{
    double? result;
    string userInput = ReadLine();
    try
    {
        result = double.Parse(userInput);
    }
    catch
    {
        result = null;
    }
    return result;
}
```
```

5. Execute the application and enter values for two vectors. The sample output is shown in Figure 12-1.

![](bbox=[0.15, 0.55, 0.82, 0.73])

FIGURE 12-1

6. Execute the application again, but this time skip at least one of the four values. The sample output is shown in Figure 12-2.

![](bbox=[0.15, 0.9, 0.82, 0.97])

FIGURE 12-2