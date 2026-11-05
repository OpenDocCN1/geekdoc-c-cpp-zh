
## Chapter 19: DateTime Methods

### Section 19.1: DateTime Formatting

#### Standard DateTime Formatting

DateTimeFormatInfo specifies a set of specifiers for simple date and time formatting. Every specifier correspond to a particular DateTimeFormatInfo format pattern.

```
//Create datetime
DateTime dt = new DateTime(2016,08,01,18,50,23,230);

var t = String.Format("{0:t}", dt); // "6:50 PM"                              ShortTime
var d = String.Format("{0:d}", dt); // "8/1/2016"                             ShortDate
var T = String.Format("{0:T}", dt); // "6:50:23 PM"                          LongTime
var D = String.Format("{0:D}", dt); // "Monday, August 1, 2016"              LongDate
var f = String.Format("{0:f}", dt); // "Monday, August 1, 2016 6:50 PM"      LongDate+ShortTime
var F = String.Format("{0:F}", dt); // "Monday, August 1, 2016 6:50:23 PM"   FullDateTime
var g = String.Format("{0:g}", dt); // "8/1/2016 6:50 PM"                    ShortDate+ShortTime
var G = String.Format("{0:G}", dt); // "8/1/2016 6:50:23 PM"                 ShortDate+LongTime
var m = String.Format("{0:m}", dt); // "August 1"                            MonthDay
var y = String.Format("{0:y}", dt); // "August 2016"                         YearMonth
var r = String.Format("{0:r}", dt); // "Mon, 01 Aug 2016 18:50:23 GMT"      RFC1123
var s = String.Format("{0:s}", dt); // "2016-08-01T18:50:23"                 SortableDateTime
var u = String.Format("{0:u}", dt); // "2016-08-01 18:50:23Z" UniversalSortableDateTime
```

#### Custom DateTime Formatting

There are following custom format specifiers:

- y (year)
- M (month)
- d (day)
- h (hour 12)
- H (hour 24)
- m (minute)
- s (second)
- f (second fraction)
- F (second fraction, trailing zeroes are trimmed)
- t (P.M or A.M)
- z (time zone)

```
var year =        String.Format("{0:y yy yyy yyyy}", dt); // "16 16 2016 2016"  year
var month =       String.Format("{0:M MM MMM MMMM}", dt); // "8 08 Aug August"  month
var day =         String.Format("{0:d dd ddd dddd}", dt); // "1 01 Mon Monday"  day
var hour =        String.Format("{0:h hh H HH}", dt);     // "6 06 18 18"      hour 12/24
var minute =      String.Format("{0:m mm}", dt);          // "50 50"           minute
var second =      String.Format("{0:s ss}", dt);          // "23 23"           second
var fraction =    String.Format("{0:f ff fff ffff}", dt); // "2 23 230 2300"   sec.fraction
var fraction2 =   String.Format("{0:F FF FFF FFFF}", dt); // "2 23 230 2300"   without zeroes
var period =      String.Format("{0:t tt}", dt);          // "P PM"            A.M. or P.M.
var zone =        String.Format("{0:z zz zzz}", dt);      // "+0 +00 +00:00"   time zone
```

You can use also date separator / (slash) and time separator : (colon).

For code example

For more information MSDN.

### Section 19.2: DateTime.AddDays(Double)

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

### Section 19.3: DateTime.AddHours(Double)

```
double[] hours = { .08333, .16667, .25, .33333, .5, .66667, 1, 2,
    29, 30, 31, 90, 365};
DateTime dateValue = new DateTime(2009, 3, 1, 12, 0, 0);
foreach (double hour in hours)
    Console.WriteLine("{0} + {1} hour(s) = {2}", dateValue, hour,
        dateValue.AddHours(hour));
```

### Section 19.4: DateTime.Parse(String)

// Converts the string representation of a date and time to its DateTime equivalent
var dateTime = DateTime.Parse("14:23 22 Jul 2016");
Console.WriteLine(dateTime.ToString());

### Section 19.5: DateTime.TryParse(String, DateTime)

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
? $"was parsed to {dateTime}"
: "can't be parsed to DateTime");
Console.WriteLine(result);
}

### Section 19.6: DateTime.AddMilliseconds(Double)

```
string dateFormat = "MM/dd/yyyy hh:mm:ss.fffffff";
DateTime date1 = new DateTime(2010, 9, 8, 16, 0, 0);
Console.WriteLine("Original date: {0} ({1:N0} ticks)\n",
    date1.ToString(dateFormat), date1.Ticks);

DateTime date2 = date1.AddMilliseconds(1);
Console.WriteLine("Second date: {0} ({1:N0} ticks)",
    date2.ToString(dateFormat), date2.Ticks);
Console.WriteLine("Difference between dates: {0} ({1:N0} ticks)\n",
    date2 - date1, date2.Ticks - date1.Ticks);

DateTime date3 = date1.AddMilliseconds(1.5);
Console.WriteLine("Third date: {0} ({1:N0} ticks)",
    date3.ToString(dateFormat), date3.Ticks);
Console.WriteLine("Difference between dates: {0} ({1:N0} ticks)",
    date3 - date1, date3.Ticks - date1.Ticks);
```

### Section 19.7: DateTime.Compare(DateTime t1, DateTime t2 )

```
DateTime date1 = new DateTime(2009, 8, 1, 0, 0, 0);
DateTime date2 = new DateTime(2009, 8, 1, 12, 0, 0);
int result = DateTime.Compare(date1, date2);
string relationship;

if (result < 0)
    relationship = "is earlier than";
else if (result == 0)
    relationship = "is the same time as";
else
    relationship = "is later than";

Console.WriteLine("{0} {1} {2}", date1, relationship, date2);
```

### Section 19.8: DateTime.DaysInMonth(Int32, Int32)

```
const int July = 7;
const int Feb = 2;

int daysInJuly = System.DateTime.DaysInMonth(2001, July);
Console.WriteLine(daysInJuly);

// daysInFeb gets 28 because the year 1998 was not a leap year.
int daysInFeb = System.DateTime.DaysInMonth(1998, Feb);
Console.WriteLine(daysInFeb);

// daysInFebLeap gets 29 because the year 1996 was a leap year.
int daysInFebLeap = System.DateTime.DaysInMonth(1996, Feb);
Console.WriteLine(daysInFebLeap);
```

### Section 19.9: DateTime.AddYears(Int32)

Add years on the dateTime object:

```
DateTime baseDate = new DateTime(2000, 2, 29);
Console.WriteLine("Base Date: {0:d}\n", baseDate);

// Show dates of previous fifteen years.
for (int ctr = -1; ctr >= -15; ctr--)
{
    Console.WriteLine("{0,2} year(s) ago: {1:d}",
        Math.Abs(ctr), baseDate.AddYears(ctr));
}

Console.WriteLine();

// Show dates of next fifteen years.
for (int ctr = 1; ctr <= 15; ctr++)
{
    Console.WriteLine("{0,2} year(s) from now: {1:d}",
        ctr, baseDate.AddYears(ctr));
}
```

### Section 19.10: Pure functions warning when dealing with DateTime

Wikipedia currently defines a pure function as follows:

- 1. The function always evaluates the same result value given the same argument value(s). The function result value cannot depend on any hidden information or state that may change while program execution proceeds or between different executions of the program, nor can it depend on any external input from I/O devices.
- 2. Evaluation of the result does not cause any semantically observable side effect or output, such as mutation of mutable objects or output to I/O devices

As a developer you need to be aware of pure methods and you will stumble upon these a lot in many areas. One I have seen that bites many junior developers is working with DateTime class methods. A lot of these are pure and if you are unaware of these you can be in for a suprise. An example:

```
DateTime sample = new DateTime(2016, 12, 25);
sample.AddDays(1);
Console.WriteLine(sample.ToShortDateString());
```

Given the example above one may expect the result printed to console to be '26/12/2016' but in reality you end up with the same date. This is because AddDays is a pure method and does not affect the original date. To get the expected output you would have to modify the AddDays call to the following:

```
sample = sample.AddDays(1);
```

### Section 19.11: DateTime.TryParseExact(String, String, IFormatProvider, DateTimeStyles, DateTime)

Converts the specified string representation of a date and time to its DateTime equivalent using the specified format, culture-specific format information, and style. The format of the string representation must match the specified format exactly. The method returns a value that indicates whether the conversion succeeded.

For Example

```
CultureInfo enUS = new CultureInfo("en-US");
```
