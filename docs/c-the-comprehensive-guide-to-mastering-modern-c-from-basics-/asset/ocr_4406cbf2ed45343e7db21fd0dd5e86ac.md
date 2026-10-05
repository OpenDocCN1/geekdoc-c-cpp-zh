# 28.4 Mathematical

28.4.1 Fraction and Time: “<ratio>” and “<chrono>” To work with time, you need

<chrono> header. Everything in it is in its own namespace, std::std::chrono introduces central time units for seconds and milliseconds, but also hours and days. All of this is heavily based on compile-time fractions that come from the <ratio> Why? Because, for example, one second is the same as 1/86400 day—and the compiler automatically converts things from <ratio> and <chrono> for you. uses <ratio> as a foundation, and you could say it represents an example usage.

<chrono> contains types and functions for the following aspects:

+   * Time spans, the difference between points in time

+   * Points in time for relative comparison to obtain time spans

+   * Clocks with different reference times such as the computer's time or GPS

+   * Calendars for date calculation and representation

+   * Time zones for converting clocks and calendars between different locations around the world

# Motivation

Imagine you saw the following line in the code:

```
sleep(10); // what unit is meant?
```

What does it tell you? It waits. How long? Ten milliseconds? Ten seconds? Experience suggests that one of the two is likely; less likely is 10 nanoseconds or 10 minutes. But according to the rule that source code should be self-explanatory and ideally without comments, it is possible with <chrono> to write the following: