```
{
    result = (T) Enum.ToObject(typeof(T), To(input, Convert.ToInt32(defaultValue)));
}
else
{
    result = (T) Convert.ChangeType(input, typeof(T));
}
}
catch (Exception ex)
{
    Tracer.Current.LogException(ex);
}

    return result;
}

// <summary>
// Converts input to Type of typeparam T
// </summary>
// <typeparam name=\"T\">typeparam is the type in which value will be returned, it could be any type eg. int, string, bool, decimal etc.</typeparam>
// <param name=\"input\">Input that need to be converted to specified type</param>
// <returns>Input is converted in Type of default value or given as typeparam T and returned</returns>
public static T To<T>(object input)
{
    return To(input, default(T));
}
```

Usages:

```
std.Name = Cast.To<string>(drConnection[\"Name\"]);
std.Age = Cast.To<int>(drConnection[\"Age\"]);
std.IsPassed = Cast.To<bool>(drConnection[\"IsPassed\"]);

// Casting type using default value
//Following both ways are correct
// Way 1 (In following style input is converted into type of default value)
std.Name = Cast.To(drConnection[\"Name\"], \"\");
std.Marks = Cast.To(drConnection[\"Marks\"], 0);
// Way 2
std.Name = Cast.To<string>(drConnection[\"Name\"], \"\");
std.Marks = Cast.To<int>(drConnection[\"Marks\"], 0);
```

# Section 59.20: Configuration reader with generic type casting

```
// <summary>
// Read configuration values from app.config and convert to specified types
// </summary>
public static class ConfigurationReader
{
    // <summary>
    // Get value from AppSettings by key, convert to Type of default value or typeparam T and
return
```