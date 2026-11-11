
可以使用 `Stream` 类的静态 `concat` 方法连接两个流：

```java
Stream<String> combined = Stream.concat(
    letters("Hello"), letters("World"));
// Yields the stream ["H", "e", "l", "l", "o", "W", "o", "r", "l", "d"]
```

当然，第一个流不应该是无限的——否则第二个流将永远没有机会。

**java.util.stream.Stream 8**

- `Stream<T> limit(long maxSize)`  
  产生一个流，包含此流中最多 maxSize 个初始元素。
- `Stream<T> skip(long n)`  
  产生一个流，其元素为此流中除前 n 个元素之外的所有元素。
- `static <T> Stream<T> concat(Stream<? extends T> a, Stream<? extends T> b)`  
  产生一个流，其元素依次为 a 的元素后跟 b 的元素。

## 1.5 其他流转换

`distinct` 方法返回一个流，它按相同顺序产生原始流中的元素，但会抑制重复元素。显然，该流必须记住已经见过的元素。

```java
Stream<String> uniqueWords
    = Stream.of("merrily", "merrily", "gently").distinct();
// Only one "merrily" is retained
```

对于流排序，`sorted` 方法有几种变体。一种适用于 `Comparable` 元素的流，另一种接受 `Comparator`。这里，我们对字符串排序，使最长的字符串排在前面：

```java
Stream<String> longestFirst =
    words.stream().sorted(Comparator.comparing(String::length).reversed());
```

与所有流转换一样，`sorted` 方法会产生一个新流，其元素是原始流中按排序顺序排列的元素。

当然，你也可以不使用流来对集合排序。当排序过程是流管道的一部分时，`sorted` 方法很有用。

最后，`peek` 方法产生另一个流，其元素与原始流相同，但每次获取元素时都会调用一个函数。这便于调试：

`findFirst` 方法返回非空集合中的第一个值。当与 `filter` 结合使用时，它通常很有用。例如，这里我们查找第一个以字母 Q 开头的单词（如果存在）：

```java
Optional<String> startsWithQ = words.filter(s -> s.startsWith("Q")).findFirst();
```

如果你不介意任意匹配项，而不仅是第一个匹配项，请使用 `findAny` 方法。当你并行化流时，这很有效，因为流可以报告它找到的任意匹配项，而不必受限于第一个匹配项。

```java
Optional<String> startsWithQ = words.parallel().filter(s -> s.startsWith("Q")).findAny();
```

如果你只想知道是否存在匹配项，请使用 `anyMatch`。该方法接受一个谓词参数，因此你不需要使用 filter。

```java
boolean aWordStartsWithQ = words.parallel().anyMatch(s -> s.startsWith("Q"));
```

还有 `allMatch` 和 `noneMatch` 方法，如果所有元素或无元素匹配某个谓词，它们会返回 true。这些方法在并行运行时也能受益。

| `java.util.stream.Stream` | 8 |
|---|---|
| • `Optional<T> max(Comparator<? super T> comparator)`<br>• `Optional<T> min(Comparator<? super T> comparator)`<br><br>使用给定比较器定义的顺序，产生此流中的最大或最小元素；如果此流为空，则产生空 `Optional`。这些是终端操作。<br><br>• `Optional<T> findFirst()`<br>• `Optional<T> findAny()`<br><br>产生此流的第一个或任意一个元素；如果此流为空，则产生空 `Optional`。这些是终端操作。<br><br>• `boolean anyMatch(Predicate<? super T> predicate)`<br>• `boolean allMatch(Predicate<? super T> predicate)`<br>• `boolean noneMatch(Predicate<? super T> predicate)`<br><br>如果此流中任一、全部或无元素匹配给定谓词，则返回 true。这些是终端操作。 | |

## 1.7 Optional 类型

`Optional<T>` 对象是类型 T 的对象或无对象的包装器。在前一种情况下，我们说该值是*存在*的。`Optional<T>` 类型旨在作为类型 T 引用的更安全替代方案，该引用要么指向一个对象，要么为 null。然而，只有正确使用它才更安全。下一节将向你展示如何做到。

### 1.7.1 如何使用 Optional 值

有效使用 Optional 的关键是使用这样一种方法：如果值不存在，则产生一个替代值；或者仅当值存在时才消费该值。

让我们看看第一种策略。通常，在没有匹配项时你会想使用一个默认值，也许是空字符串：

```java
String result = optionalString.orElse("");
// The wrapped string, or "" if none
```

你也可以调用代码来计算默认值：

```java
String result = optionalString.orElseGet(() -> locale.getDefault().getDisplayName());
// The function is only called when needed
```

或者，如果没有值，你可以抛出异常：

```java
String result = optionalString.orElseThrow(IllegalStateException::new);
// Supply a method that yields an exception object
```

你刚刚看到了在没有值存在时如何产生替代值。处理 Optional 值的另一种策略是仅当值存在时才消费该值。

`ifPresent` 方法接受一个函数。如果 Optional 值存在，它会被传递给该函数。否则，什么也不发生。

```java
optionalValue.ifPresent(v -> process(v));
```

例如，如果值存在，你想将该值添加到一个集合中，请调用

```java
optionalValue.ifPresent(v -> results.add(v));
```

或者简单地

```java
optionalValue.ifPresent(results::add);
```

调用 `ifPresent` 时，函数不会返回任何值。如果你想处理函数结果，请改用 `map`：

```java
Optional<Boolean> added = optionalValue.map(results::add);
```

现在，added 有三种值之一：如果 optionalValue 存在，则为包装到 Optional 中的 true 或 false；否则为空 Optional。

> **注意：** 这个 `map` 方法是你在第 1.3 节“filter、map 和 flatMap 方法”（第 9 页）中见过的 `Stream` 接口的 `map` 方法的类似物。只需将 Optional 值想象为大小为 0 或 1 的流。结果的大小也是 0 或 1；在后一种情况下，函数已经被应用。

**java.util.Optional**

- `T orElse(T other)`  
  产生此 Optional 的值；如果此 Optional 为空，则产生 other。
- `T orElseGet(Supplier<? extends T> other)`  
  产生此 Optional 的值；如果此 Optional 为空，则产生调用 other 的结果。
- `<X extends Throwable> T orElseThrow(Supplier<? extends X> exceptionSupplier)`  
  产生此 Optional 的值；如果此 Optional 为空，则抛出调用 exceptionSupplier 的结果。
- `void ifPresent(Consumer<? super T> consumer)`  
  如果此 Optional 非空，则将其值传递给 consumer。
- `<U> Optional<U> map(Function<? super T, ? extends U> mapper)`  
  如果此 Optional 非空且结果不为 null，则产生将此 Optional 的值传递给 mapper 的结果；否则产生空 Optional。

### 1.7.2 如何不正确地使用 Optional 值

如果你没有正确使用 Optional 值，那么相比过去“某个值或 null”的方法，你得不到任何好处。

`get` 方法获取 Optional 值中包装的元素（如果存在）；如果不存在，则抛出 `NoSuchElementException`。因此，

```java
Optional<T> optionalValue = ...;
optionalValue.get().someMethod();
```

并不比以下代码更安全：

```java
T value = ...;
value.someMethod();
```

`isPresent` 方法报告一个 `Optional<T>` 对象是否有值。但是

```java
if (optionalValue.isPresent()) optionalValue.get().someMethod();
```

并不比以下代码更简单：

```java
if (value != null) value.someMethod();
```

**java.util.Optional 8**

| 方法 | 描述 |
|---|---|
| `T get()` | 产生此 `Optional` 的值；如果为空，则抛出 `NoSuchElementException`。 |
| `boolean isPresent()` | 如果此 `Optional` 不为空，则返回 `true`。 |

### 1.7.3 创建 Optional 值

到目前为止，我们讨论了如何使用别人创建的 `Optional` 对象。如果你想编写一个创建 `Optional` 对象的方法，有几种用于此目的的静态方法，包括 `Optional.of(result)` 和 `Optional.empty()`。例如，

```java
public static Optional<Double> inverse(Double x)
{
    return x == 0 ? Optional.empty() : Optional.of(1 / x);
}
```

`ofNullable` 方法旨在作为从可能为 `null` 的值到 Optional 值的桥梁。如果 `ob` 不为 null，`Optional.ofNullable(ob)` 返回 `Optional.of(ob)`；否则返回 `Optional.empty()`。

**java.util.Optional 8**

| 方法 | 描述 |
|---|---|
| `static <T> Optional<T> of(T value)` | 产生一个包含给定值的 `Optional`。如果 `value` 为 null，此方法抛出 `NullPointerException`。 |
| `static <T> Optional<T> ofNullable(T value)` | 产生一个包含给定值的 `Optional`。如果 `value` 为 null，此方法产生一个空 `Optional`。 |
| `static <T> Optional<T> empty()` | 产生一个空 `Optional`。 |

### 1.7.4 使用 flatMap 组合 Optional 值函数

假设你有一个方法 `f` 产生 `Optional<T>`，并且目标类型 `T` 有一个方法 `g` 产生 `Optional<U>`。如果它们是普通方法，你可以通过调用 `s.f().g()` 来组合它们。但这种组合行不通，因为 `s.f()` 的类型是 `Optional<T>`，而不是 `T`。相反，应调用

```java
Optional<U> result = s.f().flatMap(T::g);
```
