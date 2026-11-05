For code example

For more information MSDN.

# Section 19.2: DateTime.AddDays(Double)

Add days into a dateTime object.

```
DateTime today = DateTime.Now;
DateTime answer = today.AddDays(36);
Console.WriteLine("Today: {0:dddd}", today);
Console.WriteLine("36 days from today: {0:dddd}", answer);
```

You also can subtract days passing a negative value:

```
DateTime today = DateTime.Now;
DateTime answer = today.AddDays(-3);
Console.WriteLine("Today: {0:dddd}", today);
Console.WriteLine("-3 days from today: {0:dddd}", answer);
```

# Section 19.3: DateTime.AddHours(Double)

```
double[] hours = { .08333, .16667, .25, .33333, .5, .66667, 1, 2,
    29, 30, 31, 90, 365};
DateTime dateValue = new DateTime(2009, 3, 1, 12, 0, 0);
foreach (double hour in hours)
    Console.WriteLine("{0} + {1} hour(s) = {2}", dateValue, hour,
        dateValue.AddHours(hour));
```

# Section 19.4: DateTime.Parse(String)

```
// Converts the string representation of a date and time to its DateTime equivalent
var dateTime = DateTime.Parse("14:23 22 Jul 2016");
Console.WriteLine(dateTime.ToString());
```

# Section 19.5: DateTime.TryParse(String, DateTime)

```
// Converts the specified string representation of a date and time to its DateTime equivalent and
returns a value that indicates whether the conversion succeeded
string[] dateTimeStrings = new []{
    "14:23 22 Jul 2016",
    "99:23 2x Jul 2016",
    "22/7/2016 14:23:00"
};
foreach(var dateTimeString in dateTimeStrings){
    DateTime dateTime;
    bool wasParsed = DateTime.TryParse(dateTimeString, out dateTime);
    string result = dateTimeString +
        (wasParsed
```