
When you have a stream of objects, you can transform it to a primitive type stream with the `mapToInt`, `mapToLong`, or `mapToDouble` methods. For example, if you have a stream of strings and want to process their lengths as integers, you might as well do it in an `IntStream`:

```
Stream<String> words = ...;
IntStream lengths = words.mapToInt(String::length);
```

To convert a primitive type stream to an object stream, use the `boxed` method:

```
Stream<Integer> integers = IntStream.range(0, 100).boxed();
```

Generally, the methods on primitive type streams are analogous to those on object streams. Here are the most notable differences:

- The toArray methods return primitive type arrays.
- Methods that yield an optional result return an `OptionalInt`, `OptionalLong`, or `OptionalDouble`. These classes are analogous to the `Optional` class, but they have methods `getAsInt`, `getAsLong`, and `getAsDouble` instead of the `get` method.
- There are methods `sum`, `average`, `max`, and `min` that return the sum, average, maximum, and minimum. These methods are not defined for object streams.
- The `summaryStatistics` method yields an object of type `IntSummaryStatistics`, `LongSummaryStatistics`, or `DoubleSummaryStatistics` that can simultaneously report the sum, count, average, maximum, and minimum of the stream.

> **NOTE:** The `Random` class has methods `ints`, `longs`, and `doubles` that return primitive type streams of random numbers. If you need random numbers in parallel streams, use the `SplittableRandom` class instead.

The program in Listing 1.7 gives examples for the API of primitive type streams.

```
Listing 1.7 streams/PrimitiveTypeStreams.java

1 package streams;
2
3 /**
4  * @version 1.01 2018-05-01
5  * @author Cay Horstmann
6  */
7
8 import java.io.IOException;
9 import java.nio.charset.StandardCharsets;
10 import java.nio.file.Files;
11 import java.nio.file.Path;
12 import java.nio.file.Paths;
13 import java.util.stream.Collectors;
14 import java.util.stream.IntStream;
15 import java.util.stream.Stream;
16
17 public class PrimitiveTypeStreams
18 {
19     public static void show(String title, IntStream stream)
20     {
21         final int SIZE = 10;
22         int[] firstElements = stream.limit(SIZE + 1).toArray();
23         System.out.print(title + " : ");
24         for (int i = 0; i < firstElements.length; i++)
25         {
26             if (i > 0) System.out.print(", ");
27             if (i < SIZE) System.out.print(firstElements[i]);
28             else System.out.print("...");
29         }
30         System.out.println();
31     }
32
33     public static void main(String[] args) throws IOException
34     {
35         IntStream is1 = IntStream.generate(() -> (int) (Math.random() * 100));
36         show("is1", is1);
37         IntStream is2 = IntStream.range(5, 10);
38         show("is2", is2);
39         IntStream is3 = IntStream.rangeClosed(5, 10);
40         show("is3", is3);
41
42         Path path = Paths.get("../gutenberg/alice30.txt");
43         var contents = Files.readString(path);
44
45         Stream<String> words = Stream.of(contents.split("\\PL+"));
46         IntStream is4 = words.mapToInt(String::length);
47         show("is4", is4);
48         var sentence = "\uD835\uDD46 is the set of octonions.";
49         System.out.println(sentence);
50         IntStream codes = sentence.codePoints();
51         System.out.println(codes.mapToObj(c -> String.format("%X ", c)).collect(
52             Collectors.joining()));
53
54         Stream<Integer> integers = IntStream.range(0, 100).boxed();
55         IntStream is5 = integers.mapToInt(Integer::intValue);
56         show("is5", is5);
57     }
58 }
```

### java.util.stream.IntStream 8

- `static IntStream range(int startInclusive, int endExclusive)`
- `static IntStream rangeClosed(int startInclusive, int endInclusive)`
  yields an `IntStream` with the integers in the given range.
- `static IntStream of(int... values)`
  yields an `IntStream` with the given elements.
- `int[] toArray()`
  yields an array with the elements of this stream.
- `int sum()`
- `OptionalDouble average()`
- `OptionalInt max()`
- `OptionalInt min()`
- `IntSummaryStatistics summaryStatistics()`
  yields the sum, count, average, maximum, and minimum of the elements in this stream, or an object from which all five of these values can be obtained.
- `Stream<Integer> boxed()`
  yields a stream of wrapper objects for the elements in this stream.

### java.util.stream.LongStream 8

- `static LongStream range(long startInclusive, long endExclusive)`
- `static LongStream rangeClosed(long startInclusive, long endInclusive)`
  yields a `LongStream` with the integers in the given range.
- `static LongStream of(long... values)`
  yields a `LongStream` with the given elements.
- `long[] toArray()`
  yields an array with the elements of this stream.
- `long sum()`
- `OptionalDouble average()`
- `OptionalLong max()`
- `OptionalLong min()`
- `LongSummaryStatistics summaryStatistics()`
  yields the sum, count, average, maximum, and minimum of the elements in this stream, or an object from which all five of these values can be obtained.
- `Stream<Long> boxed()`
  yields a stream of wrapper objects for the elements in this stream.

### java.util.stream.DoubleStream 8

| Method | Description |
| --- | --- |
| `static DoubleStream of(double... values)` | yields a `DoubleStream` with the given elements. |
| `double[] toArray()` | yields an array with the elements of this stream. |
| `double sum()` | |
| `OptionalDouble average()` | |
| `OptionalDouble max()` | |
| `OptionalDouble min()` | |
| `DoubleSummaryStatistics summaryStatistics()` | yields the sum, count, average, maximum, and minimum of the elements in this stream, or an object from which all five of these values can be obtained. |
| `Stream<Double> boxed()` | yields a stream of wrapper objects for the elements in this stream. |

### java.lang.CharSequence 1.0

| Method | Since | Description |
| --- | --- | --- |
| `IntStream codePoints()` | 8 | yields a stream of all Unicode code points of this string. |

### java.util.Random 1.0

| Method | Since |
| --- | --- |
| `IntStream ints()` | 8 |
| `IntStream ints(int randomNumberOrigin, int randomNumberBound)` | 8 |
| `IntStream ints(long streamSize)` | 8 |
| `IntStream ints(long streamSize, int randomNumberOrigin, int randomNumberBound)` | 8 |
| `LongStream longs()` | 8 |
| `LongStream longs(long randomNumberOrigin, long randomNumberBound)` | 8 |
| `LongStream longs(long streamSize)` | 8 |
| `LongStream longs(long streamSize, long randomNumberOrigin, long randomNumberBound)` | 8 |
| `DoubleStream doubles()` | 8 |
| `DoubleStream doubles(double randomNumberOrigin, double randomNumberBound)` | 8 |
| `DoubleStream doubles(long streamSize)` | 8 |
| `DoubleStream doubles(long streamSize, double randomNumberOrigin, double randomNumberBound)` | 8 |

Yields streams of random numbers. If `streamSize` is provided, the stream is finite with the given number of elements. When bounds are provided, the elements are between `randomNumberOrigin` (inclusive) and `randomNumberBound` (exclusive).

### java.util.Optional<Int|Long|Double> 8

- `static Optional<Int|Long|Double> of((int|long|double) value)`
  yields an optional object with the supplied primitive type value.
- `(int|long|double) getAs(Int|Long|Double)()`
  yields the value of this optional object, or throws a `NoSuchElementException` if it is empty.
- `(int|long|double) orElse((int|long|double) other)`
- `(int|long|double) orElseGet((Int|Long|Double)Supplier other)`
  yields the value of this optional object, or the alternative value if this object is empty.
- `void ifPresent((Int|Long|Double)Consumer consumer)`
  If this optional object is not empty, it passes its value to consumer.

### java.util.(Int|Long|Double)SummaryStatistics 8

- `long getCount()`
- `(int|long|double) getSum()`
- `double getAverage()`
- `(int|long|double) getMax()`
- `(int|long|double) getMin()`
  yields the count, sum, average, maximum, and minimum of the collected elements.

## 1.14 Parallel Streams

Streams make it easy to parallelize bulk operations. The process is mostly automatic, but you need to follow a few rules. First of all, you must have a parallel stream. You can get a parallel stream from any collection with the `Collection.parallelStream()` method:

```
Stream<String> parallelWords = words.parallelStream();
```

Moreover, the parallel method converts any sequential stream into a parallel one.

```
Stream<String> parallelWords = Stream.of(wordArray).parallel();
```

As long as the stream is in parallel mode when the terminal method executes, all intermediate stream operations will be parallelized.
