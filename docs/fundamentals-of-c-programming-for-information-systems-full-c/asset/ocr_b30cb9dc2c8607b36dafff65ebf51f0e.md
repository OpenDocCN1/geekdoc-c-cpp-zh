| Subtract(DateTime) | Returns a TimeSpan obtained by subtracting a specified DateTime | graduationDate.Subtract(DateTime.Now): Returns a TimeSpan with the number of days, hours, and so on between now and graduation date. |
| Add(TimeSpan) | Returns the DateTime obtained by adding the specified TimeSpan to a DateTime | DateTime.Now.Add(fillTime)*: Returns the DateTime value obtained by adding 3 days, 2 hours and 30 minutes to current date and time.
*fillTime: (3, 2, 30, 0, 0) |

# Computing the difference between two dates

.Net Framework uses a TimeSpan structure to represent the time interval between two DateTime values.

# TimeSpan structure

To get the difference between two DateTime values, you may subtract one from the other. For example, the time to graduate may be computed and stored in a TimeSpan variable as follows:

```
TimeSpan timeToGraduate = gradDate-DateTime.Now;
```

Table 2-11 shows commonly used properties of TimeSpan Stucture.

# Table 2-11: Properties of TimeSpan stucture

| Properties of TimeSpan | Description |
| Days, Hours, Minutes, Seconds, Milliseconds, Ticks | The number of whole days and remaining whole hours, minutes, seconds, milliseconds and ticks in a time interval.
For example, the TimeSpan representing (#12/19/2017 4:40:45 PM# - #12/18/2017 1:10:30 PM#) would have following values for its properties:
Days - 1
Hours - 3
Minutes - 30
Seconds - 15 |
| TotalDays, TotalHours, TotalMinutes, TotalSeconds, TotalMilliSeconds | Each property returns the entire interval expressed in a particular unit like days, hours or minutes. For example, the TimeSpan representing (#12/19/2015 4:30:45 PM# - #12/18/2015 1:20:40 PM#) would have following values for its properties:
TotalDays - 1.146 (0.146 represents the fractional days)
TotalHours - 27.504 (includes 27 days and .504 fractional hours)
TotalMinutes - 1650.25 |

A TimeSpan also may be created using the new key word:

```
TimeSpan variableName = new TimeSpan(days, hours, minutes, seconds, milliseconds);
```

Here is a specific example of a TimeSpan that represents the time it takes to fill an order: 2 days, 3 hours and 30 minutes:

```
TimeSpan fillTime = new TimeSpan(2, 3, 30, 0, 0);
```