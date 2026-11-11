
*This page intentionally left blank*

## CHAPTER 6: The Date and Time API

### In this chapter

- 6.1 The Time Line, page 354
- 6.2 Local Dates, page 358
- 6.3 Date Adjusters, page 364
- 6.4 Local Time, page 365
- 6.5 Zoned Time, page 367
- 6.6 Formatting and Parsing, page 371
- 6.7 Interoperating with Legacy Code, page 376

Time flies like an arrow, and we can easily set a starting point and count forward and backward in seconds. So why is it so hard to deal with time? The problem is humans. All would be easy if we could just tell each other: “Meet me at 1523793600, and don’t be late!” But we want time to relate to daylight and the seasons. That’s where things get complicated. Java 1.0 had a `Date` class that was, in hindsight, naive, and had most of its methods deprecated in Java 1.1 when a calendar class was introduced. Its API wasn’t stellar, its instances were mutable, and it didn’t deal with issues such as leap seconds. The third time is a charm, and the `java.time` API introduced in Java 8 has remedied the flaws of the past and should serve us for quite some time. In this chapter, you will learn what makes time computations so vexing, and how the Date and Time API solves these issues.

The static method `Instant.now()` gives the current instant. You can compare two instants with the equals and compareTo methods in the usual way, so you can use instants as timestamps.

To find out the difference between two instants, use the static method `Duration.between`. For example, here is how you can measure the running time of an algorithm:

```java
Instant start = Instant.now();
runAlgorithm();
Instant end = Instant.now();
Duration timeElapsed = Duration.between(start, end);
long millis = timeElapsed.toMillis();
```

A Duration is the amount of time between two instants. You can get the length of a Duration in conventional units by calling `toNanos`, `toMillis`, `toSeconds`, `toMinutes`, `toHours`, or `toDays`.

> **NOTE:** In Java 8, you had to call `getSeconds` instead of `toSeconds`.

If you need nanosecond precision, be aware of overflow. A long value can hold almost 300 years of nanoseconds. If your durations are shorter than that, simply convert them to nanoseconds. You can use longer durations—a `Duration` object stores the number of seconds in a long, and the number of nanoseconds in an additional int. The Duration API has a number of methods, shown at the end of this section, for carrying out arithmetic.

For example, if you want to check whether an algorithm is at least ten times faster than another, you can compute

```java
Duration timeElapsed2 = Duration.between(start2, end2);
boolean overTenTimes
    = timeElapsed.multipliedBy(10).minus(timeElapsed2).isNegative();
```

This is just to show the syntax. Since the algorithms aren’t going to run for hundreds of years, you can simply use

```java
boolean overTenTimesFaster = timeElapsed.toNanos() * 10 < timeElapsed2.toNanos();
```

> **NOTE:** The Instant and Duration classes are immutable, and all methods, such as multipliedBy or minus, return a new instance.

```java
42
43 public static void runAlgorithm2()
44 {
45     int size = 10;
46     List<Integer> list = new Random().ints(1, 100).map(i -> i % 100).limit(size)
47         .boxed().collect(Collectors.toList());
48     while (!IntStream.range(1, list.size())
49         .allMatch(i -> list.get(i - 1).compareTo(list.get(i)) <= 0))
50         Collections.shuffle(list);
51     System.out.println(list);
52 }
53 }
```

| java.time.Instant 8 |
| --- |
| • static Instant now()<br>gets the current instant from the best available system clock. |
| • Instant plus(TemporalAmount amountToAdd)<br>• Instant minus(TemporalAmount amountToSubtract)<br>yields an instant that is the given amount away from this Instant. The classes Duration and Period (see Section 6.2, “Local Dates,” on p. 358) implement the TemporalAmount interface. |
| • Instant (plus\|minus)(Nanos\|Millis\|Seconds)(long number)<br>yields an Instant that is the given number of nanoseconds, milliseconds, or seconds away from this Instant. |

| java.time.Duration 8 |
| --- |
| • static Duration of(Nanos\|Millis\|Seconds\|Minutes\|Hours\|Days)(long number)<br>yields a duration of the given number of time units. |
| • static Duration between(Temporal startInclusive, Temporal endExclusive)<br>yields a duration between the given points in time. The Temporal interface is implemented by the Instant class as well as LocalDate/LocalDateTime/LocalTime (see Section 6.4, “Local Time,” on p. 365) and ZonedDateTime (see Section 6.5, “Zoned Time,” on p. 367). |

### Listing 6.2 `localdates/LocalDates.java`

```java
package localdates;

/**
 * @version 1.0 2016-05-10
 * @author Cay Horstmann
 */
import java.time.*;
import java.time.temporal.*;
import java.util.stream.*;

public class LocalDates
{
    public static void main(String[] args)
    {
        LocalDate today = LocalDate.now(); // Today's date
        System.out.println("today: " + today);

        LocalDate alonzosBirthday = LocalDate.of(1903, 6, 14);
        alonzosBirthday = LocalDate.of(1903, Month.JUNE, 14);
        // Uses the Month enumeration
        System.out.println("alonzosBirthday: " + alonzosBirthday);

        LocalDate programmersDay = LocalDate.of(2018, 1, 1).plusDays(255);
        // September 13, but in a leap year it would be September 12
        System.out.println("programmersDay: " + programmersDay);

        LocalDate independenceDay = LocalDate.of(2018, Month.JULY, 4);
        LocalDate christmas = LocalDate.of(2018, Month.DECEMBER, 25);

        System.out.println("Until christmas: " + independenceDay.until(christmas));
        System.out.println("Until christmas: "
                + independenceDay.until(christmas, ChronoUnit.DAYS));

        System.out.println(LocalDate.of(2016, 1, 31).plusMonths(1));
        System.out.println(LocalDate.of(2016, 3, 31).minusMonths(1));

        DayOfWeek startOfLastMillennium = LocalDate.of(1900, 1, 1).getDayOfWeek();
        System.out.println("startOfLastMillennium: " + startOfLastMillennium);
        System.out.println(startOfLastMillennium.getValue());
        System.out.println(DayOfWeek.SATURDAY.plus(3));

        LocalDate start = LocalDate.of(2000, 1, 1);
        LocalDate endExclusive = LocalDate.now();
        Stream<LocalDate> firstDaysInMonth = start.datesUntil(endExclusive, Period.ofMonths(1));
        System.out.println("firstDaysInMonth: "
                + firstDaysInMonth.collect(Collectors.toList()));
    }
}
```

### java.time.LocalDate 8

- `static LocalDate now()`  
  gets the current LocalDate.
- `static LocalDate of(int year, int month, int dayOfMonth)`
- `static LocalDate of(int year, Month month, int dayOfMonth)`  
  yields a local date with the given year, month (as integer between 1 and 12 or a value of the Month enumeration), and day of the month (between 1 and 31).
- `LocalDate (plus|minus)(Days|Weeks|Months|Years)(long number)`  
  yields a LocalDate obtained by adding or subtracting the given number of time units.
- `LocalDate plus(TemporalAmount amountToAdd)`
- `LocalDate minus(TemporalAmount amountToSubtract)`  
  yields a LocalDate that is the given amount away from this LocalDate. The classes Duration and Period implement the TemporalAmount interface.
- `LocalDate withDayOfMonth(int dayOfMonth)`
- `LocalDate withDayOfYear(int dayOfYear)`
- `LocalDate withMonth(int month)`
- `LocalDate withYear(int year)`  
  returns a new LocalDate with the day of month, day of year, month, or year changed to the given value.
- `int getDayOfMonth()`  
  gets the day of the month (between 1 and 31).
- `int getDayOfYear()`  
  gets the day of the year (between 1 and 366).
- `DayOfWeek getDayOfWeek()`  
  gets the day of the week, returning a value of the DayOfWeek enumeration.
- `Month getMonth()`
- `int getMonthValue()`  
  gets the month as a value of the Month enumeration, or as a number between 1 and 12.
- `int getYear()`  
  gets the year, between -999,999,999 and 999,999,999.
- `Period until(ChronoLocalDate endDateExclusive)`  
  gets the period until the given end date. The ChronoLocalDate interface is implemented by LocalDate and date classes for non-Gregorian calendars.
