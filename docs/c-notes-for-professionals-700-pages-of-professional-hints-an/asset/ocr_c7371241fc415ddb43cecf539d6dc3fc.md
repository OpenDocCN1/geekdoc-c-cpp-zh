Let's say we have a Date string, example like '23-12-2016' or '12/23/2016' and we want it to convert to equivalent DateTime object, without any specific culture information

```
```csharp
string date = '23-12-2016' or date = 12/23/2016';
string[] formats = new string[] {"dd-MM-yyyy","MM/dd/yyyy"}; // even can add more possible
formats.
DateTime date = DateTime.ParseExact(date, formats,
CultureInfo.InvariantCulture,DateTimeStyles.None);
```
```

**NOTE : System.Globalization needs to be added for CultureInfo Class**

# ## Section 19.16: DateTime ToString, ToShortDateString, ToLongDateString and ToString formatted

```
```csharp
using System;

public class Program
{
    public static void Main()
    {
        var date = new DateTime(2016,12,31);

        Console.WriteLine(date.ToString());        //Outputs: 12/31/2016 12:00:00 AM
        Console.WriteLine(date.ToShortDateString()); //Outputs: 12/31/2016
        Console.WriteLine(date.ToLongDateString()); //Outputs: Saturday, December 31, 2016
        Console.WriteLine(date.ToString("dd/MM/yyyy"));    //Outputs: 31/12/2016
    }
}
```
```

# ## Section 19.17: Current Date

To get the current date you use the DateTime.Today property. This returns a DateTime object with today's date. When this is then converted .ToString() it is done so in your system's locality by default.

For example:

```
```csharp
Console.WriteLine(DateTime.Today);
```
```

Writes today's date, in your local format to the console.