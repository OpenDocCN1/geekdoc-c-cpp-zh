# Section 19.9: DateTime.AddYears(Int32)

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

# Section 19.10: Pure functions warning when dealing with DateTime

Wikipedia currently defines a pure function as follows:

+   1. The function always evaluates the same result value given the same argument value(s). The function result value cannot depend on any hidden information or state that may change while program execution proceeds or between different executions of the program, nor can it depend on any external input from I/O devices.
+   2. Evaluation of the result does not cause any semantically observable side effect or output, such as mutation of mutable objects or output to I/O devices

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

# Section 19.11: DateTime.TryParseExact(String,\String,\IFormatProvider,\DateTimeStyles,\DateTime)

Converts the specified string representation of a date and time to its DateTime equivalent using the specified format, culture-specific format information, and style. The format of the string representation must match the specified format exactly. The method returns a value that indicates whether the conversion succeeded.

For Example

```
CultureInfo enUS = new CultureInfo("en-US");
```