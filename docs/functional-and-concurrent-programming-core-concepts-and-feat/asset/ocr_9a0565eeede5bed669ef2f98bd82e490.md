# # Chapter 10 Standard Higher-Order Functions

```
```scala
val points: List[(Double, Double)] = ...
points.sortBy((x, y) => x * x + y * y)
```
```

Again, the result is a list of points, not a list of distances.

```
```scala
val temps: List[Int] = ...
val datedTemps: List[(LocalDate, Int)] = ...
temps.max // highest temperature
datedTemps.max // highest temperature on the last date
```
```

Note that the second expression needs to compare pairs. The default behavior, in Scala, is to compare them in lexicographic order—that is, according to the first component, or the second component if the first components are equal. As a result, datedTemps.max finds the last (highest) date, and within this date, the highest temperature. To retrieve the highest temperature overall, ignoring dates, use maxBy:

```
```scala
datedTemps.maxBy((_, temp) => temp) // highest temperature overall
```
```

To get the highest temperature overall, but pick its earliest date if it occurs multiple times, is a little more complicated:

```
```scala
val byTemp: Ordering[(LocalDate, Int)] = Ordering.by((_, temp) => temp)
val byDate: Ordering[(LocalDate, Int)] = Ordering.by((date, _) => date)
datedTemps.max(byTemp.orElse(byDate.reverse))
```
```

Note the use of a higher-order function by to build ordering objects, which are then combined to sort dated temperatures according to temperatures first, and for equal temperatures, by reverse order of dates.



The last standard higher-order function discussed in this chapter is groupBy, also commonly found in functional libraries (and even in Java as Collectors.groupingBy). As its name indicates, this function is used to form groups of elements from a collection.