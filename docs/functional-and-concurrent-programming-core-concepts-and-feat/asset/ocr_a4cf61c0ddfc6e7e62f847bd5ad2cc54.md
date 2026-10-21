# A.7 Handling Failures

Error handling in Java and Kotlin is still very much centered on throwing and catching exceptions. Kotlin recently introduced a `Result` type, similar to Scala’s `Try`. You could rewrite in Kotlin some of Scala’s `Try`-based code from Section 13.3:

```
```kotlin
val lines: Result<List<String>> = runCatching {
    ... // a list-producing computation
}

val linesOrNull: List<String>? = lines.getOrNull()
val linesOrEmpty: List<String> = lines.getOrDefault(listOf())
val linesOrOther: List<String> = lines.getOrElse { someListComputation() }
```
```

Value `lines` is a successful result if the computation inside `runCatching` produces a list. If instead it throws an exception, the exception is caught and wrapped into a failed result. The value inside `Result` can be extracted and replaced with a default value or with null if it is missing. (In Kotlin, a type A does not contain null, which is added in type A?; see the later discussion.)

As with `Try`, `Result` values can be transformed using higher-order functions:

```
```kotlin
fun compute(list: List<String>): Int = ...
fun computeOrFail(list: List<String>): Result<Int> = ...

lines.map { compute(it) }                         // of type Result<Int>
lines.mapCatching { computeOrFail(it).getOrThrow() } // of type Result<Int>
```
```

The second expression is simpler in Scala, but Kotlin’s `Result` type does not (yet) implement a `flatMap` method.

Java only has its `Optional` type to offer, but at least it defines a `flatMap` method:

```
```java
List<String> someListComputation() { ... }
int compute(List<String> list) { ... }
Optional<Integer> computeOrFail(List<String> list) { ... }

Optional<List<String>> lines = ...

List<String> linesOrEmpty = lines.orElse(Collections.emptyList());
List<String> linesOrOther = lines.orElseGet(() -> someListComputation());
```
```