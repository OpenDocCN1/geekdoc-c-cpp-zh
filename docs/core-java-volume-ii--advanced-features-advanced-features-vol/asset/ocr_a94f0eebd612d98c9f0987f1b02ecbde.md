Suppose you want to collect all strings in a stream by concatenating them. You can call

```
```java
String result = stream.collect(Collectors.joining());
```
```

If you want a delimiter between elements, pass it to the joining method:

```
```java
String result = stream.collect(Collectors.joining(", "));
```
```

If your stream contains objects other than strings, you need to first convert them to strings, like this:

```
```java
String result = stream.map(Object::toString).collect(Collectors.joining(", "));
```
```

If you want to reduce the stream results to a sum, count, average, maximum, or minimum, use one of the summarizing(Int|Long|Double) methods. These methods take a function that maps the stream objects to numbers and yield a result of type (Int|Long|Double)SummaryStatistics, simultaneously computing the sum, count, average, maximum, and minimum.

```
```java
IntSummaryStatistics summary = stream.collect(
    Collectors.summarizingInt(String::length));
double averageWordLength = summary.getAverage();
double maxWordLength = summary.getMax();
```
```

The example program in Listing 1.4 shows how to collect elements from a stream.

# **Listing 1.4** collecting/CollectingResults.java

```
```java
1 package collecting;
2
3 /**
4  * @version 1.01 2018-05-01
5  * @author Cay Horstmann
6  */
7
8 import java.io.*;
9 import java.nio.charset.*;
10 import java.nio.file.*;
11 import java.util.*;
12 import java.util.stream.*;
13
14 public class CollectingResults
15 {
```
```