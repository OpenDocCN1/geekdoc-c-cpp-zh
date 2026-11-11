```
```java
88    Map<String, String> stateToCityNames = cities.collect(groupingBy(
89        City::getState,
90        reducing("", City::getState, (s, t) -> s.length() == 0 ? t : s
91            + ", " + t)));
92
93    cities = readCities("cities.txt");
94    stateToCityNames = cities.collect(groupingBy(City::getState,
95        mapping(City::getName, joining(", "))));
96    System.out.println("stateToCityNames: " + stateToCityNames);
97
98 }
```
```

+   **java.util.stream.Collectors 8**
+   
+   - `static <T> Collector<T,?,Long> counting()`
+     yields a collector that counts the collected elements.
+   - `static <T> Collector<T,?,Integer> summingInt(ToIntFunction<? super T> mapper)`
+   - `static <T> Collector<T,?,Long> summingLong(ToLongFunction<? super T> mapper)`
+   - `static <T> Collector<T,?,Double> summingDouble(ToDoubleFunction<? super T> mapper)`
+     yields a collector that computes the sum of the values of applying mapper to the collected elements.
+   - `static <T> Collector<T,?,Optional<T>> maxBy(Comparator<? super T> comparator)`
+   - `static <T> Collector<T,?,Optional<T>> minBy(Comparator<? super T> comparator)`
+     yields a collector that computes the maximum or minimum of the collected elements, using the ordering specified by comparator.
+   - `static <T,U,A,R> Collector<T,?,R> mapping(Function<? super T,? extends U> mapper, Collector<? super U,A,R> downstream)`
+     yields a collector that produces a map whose keys are mapper applied to the collected elements, and whose values are the result of collecting the elements with the same key using the downstream collector.

# # 1.12 Reduction Operations

The reduce method is a general mechanism for computing a value from a stream. The simplest form takes a binary function and keeps applying it, starting with the first two elements. It’s easy to explain this if the function is the sum:

```
```java
List<Integer> values = . . . ;
Optional<Integer> sum = values.stream().reduce((x, y) -> x + y);
```
```