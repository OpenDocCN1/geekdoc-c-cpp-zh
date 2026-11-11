# java.time.LocalDate ⁸ *(Continued)*

+   - `boolean isBefore(ChronoLocalDate other)`
+   - `boolean isAfter(ChronoLocalDate other)`  
+     returns true if this date is before or after the given date.
+   - `boolean isLeapYear()`  
+     returns true if the year is a leap year—that is, if it is divisible by 4 but not by 100, or divisible by 400. The algorithm is applied for all past years, even though that is historically inaccurate. (Leap years were invented in the year −46, and the rules involving divisibility by 100 and 400 were introduced in the Gregorian calendar reform of 1582. The reform took over 300 years to become universal.)
+   - `Stream<LocalDate> datesUntil(LocalDate endExclusive)` ⁹
+   - `Stream<LocalDate> datesUntil(LocalDate endExclusive, Period step)` ⁹  
+     yields a stream of dates from this `LocalDate` until the end, with step size 1 or the given period.

# java.time.Period ⁸

+   - `static Period of(int years, int months, int days)`
+   - `Period of(Days|Weeks|Months|Years)(int number)`  
+     yields a `Period` with the given number of time units.
+   - `int get(Days|Months|Years)()`  
+     gets the days, months, or years of this `Period`.
+   - `Period (plus|minus)(Days|Months|Years)(long number)`  
+     yields a `Period` obtained by adding or subtracting the given number of time units.
+   - `Period plus(TemporalAmount amountToAdd)`
+   - `Period minus(TemporalAmount amountToSubtract)`  
+     yields an instant that is the given amount away from this `Instant`. The classes `Duration` and `Period` implement the `TemporalAmount` interface.
+   - `Period with(Days|Months|Years)(int number)`  
+     returns a new `Period` with the days, months, or years changed to the given number.