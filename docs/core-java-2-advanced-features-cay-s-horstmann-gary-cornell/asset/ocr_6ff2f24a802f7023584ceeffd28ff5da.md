```
```java
Instant start = Instant.now();
runAlgorithm();
Instant end = Instant.now();
Duration timeElapsed = Duration.between(start, end);
long millis = timeElapsed.toMillis();
```
```

A Duration is the amount of time between two instants. You can get the length of a Duration in conventional units by calling `toNanos`, `toMillis`, `getSeconds`, `toMinutes`, `toHours`, or `toDays`.

Durations require more than a long value for their internal storage. The number of seconds is stored in a long, and the number of nanoseconds in an additional int. If you want to make computations to nanosecond accuracy, and you actually need the entire range of a Duration, you can use one of the methods in Table 6.1. Otherwise, you can just call `toNanos` and do your calculations with long values.

> **NOTE:** It takes almost 300 years of nanoseconds to overflow a long.

For example, if you want to check whether an algorithm is at least ten times faster than another, you can compute

```
```java
Duration timeElapsed2 = Duration.between(start2, end2);
boolean overTenTimesFaster =
    timeElapsed2.multipliedBy(10).minus(timeElapsed2).isNegative();
// Or timeElapsed2.toNanos() < 10 * timeElapsed2.toNanos()
```
```

# Table 6.1 Arithmetic Operations for Time Instants and Durations

| Method | Description |
|---|---|
| `plus`, `minus` | Adds a duration to, or subtracts a duration from, this Instant or Duration. |
| `plusNanos`, `plusMillis`, `plusSeconds`, `minusNanos`, `minusMillis`, `minusSeconds` | Adds or subtracts a number of the given time units to this Instant or Duration. |
| `plusMinutes`, `plusHours`, `plusDays`, `minusMinutes`, `minusHours`, `minusDays` | Adds or subtracts a number of the given time units to this Duration. |
| `multipliedBy`, `dividedBy`, `negated` | Returns a duration obtained by multiplying or dividing this Duration by a given long, or by -1. Note that you can scale only durations, not instants. |
| `isZero`, `isNegative` | Checks whether this Duration is zero or negative. |