
- Methods that yield an optional result return an `OptionalInt`, `OptionalLong`, or `OptionalDouble`. These classes are analogous to the `Optional` class but have methods `getAsInt`, `getAsLong`, and `getAsDouble` instead of the get method.
- There are methods `sum`, `average`, `max`, and `min` that return the sum, average, maximum, and minimum. These methods are not defined for object streams.
- The `summaryStatistics` method yields an object of type `IntSummaryStatistics`, `LongSummaryStatistics`, or `DoubleSummaryStatistics` that can simultaneously report the sum, average, maximum, and minimum of the stream.

> **NOTE:** The `Random` class has methods `ints`, `longs`, and `doubles` that return primitive type streams of random numbers.

The program in Listing 1.7 gives examples for the API of primitive type streams.

### Listing 1.7 `streams/PrimitiveTypeStreams.java`

```java
package streams;

import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.stream.Collectors;
import java.util.stream.IntStream;
import java.util.stream.Stream;

public class PrimitiveTypeStreams
{
    public static void show(String title, IntStream stream)
    {
        final int SIZE = 10;
        int[] firstElements = stream.limit(SIZE + 1).toArray();
        System.out.print(title + ": ");
        for (int i = 0; i < firstElements.length; i++)
        {
            if (i > 0) System.out.print(", ");
            if (i < SIZE) System.out.print(firstElements[i]);
            else System.out.print("...");
        }
        System.out.println();
    }

    public static void main(String[] args) throws IOException
    {
        IntStream is1 = IntStream.generate(() -> (int) (Math.random() * 100));
        show("is1", is1);
        IntStream is2 = IntStream.range(5, 10);
        show("is2", is2);
        IntStream is3 = IntStream.rangeClosed(5, 10);
        show("is3", is3);

        Path path = Paths.get("../gutenberg/alice30.txt");
        String contents = new String(Files.readAllBytes(path), StandardCharsets.UTF_8);

        Stream<String> words = Stream.of(contents.split("\\PL+"));
        IntStream is4 = words.mapToInt(String::length);
        show("is4", is4);
        String sentence = "\uD835\uDD46 is the set of octonions.";
        System.out.println(sentence);
        IntStream codes = sentence.codePoints();
        System.out.println(codes.mapToObj(c -> String.format("%X", c)).collect(
            Collectors.joining()));

        Stream<Integer> integers = IntStream.range(0, 100).boxed();
        IntStream is5 = integers.mapToInt(Integer::intValue);
        show("is5", is5);
    }
}
```

| `java.util.stream.IntStream` | 8 |
| --- | --- |
| `static IntStream range(int startInclusive, int endExclusive)` | |
| `static IntStream rangeClosed(int startInclusive, int endInclusive)` | yields an IntStream with the integers in the given range. |
| `static IntStream of(int... values)` | yields an IntStream with the given elements. |
| `int[] toArray()` | yields an array with the elements of this stream. |
| `int sum()` | |
| `OptionalDouble average()` | |
| `OptionalInt max()` | |
| `OptionalInt min()` | |
| `IntSummaryStatistics summaryStatistics()` | yields the sum, average, maximum, or minimum of the elements in this stream, or an object from which all four of these results can be obtained. |
| `Stream<Integer> boxed()` | yields a stream of wrapper objects for the elements in this stream. |

| `java.util.stream.LongStream` | 8 |
| --- | --- |
| `static LongStream range(long startInclusive, long endExclusive)` | |
| `static LongStream rangeClosed(long startInclusive, long endInclusive)` | yields a LongStream with the integers in the given range. |
| `static LongStream of(long... values)` | yields a LongStream with the given elements. |
| `long[] toArray()` | yields an array with the elements of this stream. |
| `long sum()` | |
| `OptionalDouble average()` | |
| `OptionalLong max()` | |
| `OptionalLong min()` | |
| `LongSummaryStatistics summaryStatistics()` | yields the sum, average, maximum, or minimum of the elements in this stream, or an object from which all four of these results can be obtained. |
| `Stream<Long> boxed()` | yields a stream of wrapper objects for the elements in this stream. |

| `java.util.stream.DoubleStream` | 8 |
| --- | --- |
| `static DoubleStream of(double... values)` | yields a DoubleStream with the given elements. |
| `double[] toArray()` | yields an array with the elements of this stream. |
| `double sum()` | |
| `OptionalDouble average()` | |
| `OptionalDouble max()` | |
| `OptionalDouble min()` | |
| `DoubleSummaryStatistics summaryStatistics()` | yields the sum, average, maximum, or minimum of the elements in this stream, or an object from which all four of these results can be obtained. |
| `Stream<Double> boxed()` | yields a stream of wrapper objects for the elements in this stream. |

**java.lang.CharSequence** 1.0

- `IntStream codePoints()` 8
  - yields a stream of all Unicode code points of this string.

**java.util.Random** 1.0

- `IntStream ints()`
- `IntStream ints(int randomNumberOrigin, int randomNumberBound)` 8
- `IntStream ints(long streamSize)` 8
- `IntStream ints(long streamSize, int randomNumberOrigin, int randomNumberBound)` 8
- `LongStream longs()` 8
- `LongStream longs(long randomNumberOrigin, long randomNumberBound)` 8
- `LongStream longs(long streamSize)` 8
- `LongStream longs(long streamSize, long randomNumberOrigin, long randomNumberBound)` 8
- `DoubleStream doubles()` 8
- `DoubleStream doubles(double randomNumberOrigin, double randomNumberBound)` 8
- `DoubleStream doubles(long streamSize)` 8
- `DoubleStream doubles(long streamSize, double randomNumberOrigin, double randomNumberBound)` 8

Yields streams of random numbers. If `streamSize` is provided, the stream is finite with the given number of elements. When bounds are provided, the elements are between `randomNumberOrigin` (inclusive) and `randomNumberBound` (exclusive).

**java.util.Optional (Int|Long|Double)** 8

- `static Optional (Int|Long|Double) of((int|long|double) value)`
  yields an optional object with the supplied primitive type value.
- `(int|long|double) getAs(Int|Long|Double)()`
  yields the value of this optional object, or throws a NoSuchElementException if it is empty.
- `(int|long|double) orElse((int|long|double) other)`
- `(int|long|double) orElseGet((Int|Long|Double)Supplier other)`
  yields the value of this optional object, or the alternative value if this object is empty.
- `void ifPresent((Int|Long|Double)Consumer consumer)`
  If this optional object is not empty, passes its value to consumer.

**java.util.(Int|Long|Double)SummaryStatistics** 8

- `long getCount()`
- `(int|long|double) getSum()`
- `double getAverage()`
- `(int|long|double) getMax()`
- `(int|long|double) getMin()`
  yields the count, sum, average, maximum, and minimum of the collected elements.

## 1.14 Parallel Streams

Streams make it easy to parallelize bulk operations. The process is mostly automatic, but you need to follow a few rules. First of all, you must have a parallel stream. You can get a parallel stream from any collection with the `Collection.parallelStream()` method:

```java
Stream<String> parallelWords = words.parallelStream();
```

Moreover, the `parallel` method converts any sequential stream into a parallel one.

```java
Stream<String> parallelWords = Stream.of(wordArray).parallel();
```

As long as the stream is in parallel mode when the terminal method executes, all intermediate stream operations will be parallelized.

When stream operations run in parallel, the intent is that the same result is returned as if they had run serially. It is important that the operations can be executed in an arbitrary order.
