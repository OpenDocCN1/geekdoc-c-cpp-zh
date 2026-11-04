```
var endTime2 = startTime + elapsed;
Console.WriteLine(endTime == endTime2);
```

Different metrics can be obtained from a TimeSpan value, including the components of the value (milliseconds, seconds, minutes, hours, and days), as well as totals. Examples of both are shown in the next example:

```
Console.WriteLine(elapsed.Hours + ":" + elapsed.Minutes);
Console.WriteLine(elapsed.TotalSeconds);
```

Nicer formatting can be obtained by using format strings. The default result produced by the ToString method writes down hours, minutes, and seconds, each represented by two digits and separated by colons. If nontrivial days or milliseconds values are stored by the TimeSpan value, those are printed, as well. For example:

```
42.12:34:56.789  // 42 days, 12 hours, 34 minutes, 56 seconds, 789 milliseconds
```

Parse and TryParse methods are available, as well as their Exact variants, completely analogous to the static methods on DateTime.

# PERFORMANCE MEASUREMENTS

> Certain people are keen on performance measurements of all sorts. Others are rather skeptical about excessive practice of those when no red flags have been raised on an application's or library's performance (yet). Either way, if you have to carry out such measurements, do it in a correct way. Subtracting DateTime values doesn't cut it due to limited precision. Use of the Stopwatch class is the way to go, as you will see when we discuss the System.Diagnostics namespace in Chapter 27, "Diagnostics and Instrumentation."

# Arithmetic with DateTime Values

In the discussion about TimeSpan, you learned how the difference between two DateTime values produces a TimeSpan. Adding a DateTime and a TimeSpan, on the other hand, returns another DateTime value. For convenience, the DateTime struct also has a series of Add methods that avoid the need to create a TimeSpan value first:

```
var hundredDaysFestival = DateTime.Now.AddDays(100);
```

A single Subtract method is provided to subtract a TimeSpan from a DateTime value, mainly for use by languages that don't have operator overloading support. This shows how good API design accommodates for languages that may be missing some of the conveniences that are present in C#. In fact, operator overloading support is not in the list of Common Language Specification (CLS) compliance rules.