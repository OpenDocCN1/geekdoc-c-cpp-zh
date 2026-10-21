# A.2 Immutability

Java and Kotlin functions can be either pure or impure. For actions—functions with no return value, applied for side effects—Java has a keyword void, whereas Kotlin uses a Unit return type, like Scala. Kotlin uses var and val to define reassignable and non-reassignable variables, like Scala. In Java, variables are reassignable by default but become non-reassignable when the keyword final is used.

Kotlin lets you defer the initialization of a val variable, a feature Scala does not have:

```
Kotlin
fun parseVerbosity(arg: String): Int {
  val verbosity: Int
  if (arg == "-v") verbosity = 1
  else if (arg == "-vv") verbosity = 2
  else verbosity = 0
  return verbosity
}
```

Most Java collections are mutable. Kotlin defines immutable collection types, but they are mostly read-only views of underlying mutable implementations:

```
Kotlin
val readOnly: List<Int> = listOf(1, 2, 3)
val cheating = readOnly as MutableList<Int>
cheating[1] = 20
val x = readOnly[1] // 20
```

In this example, variable readOnly is of type List, an immutable type in Kotlin. Internally, however, it is implemented (on the JVM) as an old-fashioned array-based list. It can even be type cast to a mutable type, and modified: The second element of list readOnly is changed from 2 to 20.

This makes Kotlin lists fundamentally different from lists in Scala (or in any functional programming language). In particular, Kotlin lists have no constant-time head and tail operations:

```
Scala
val a: List[String] = List("A","B","C")
val b = a.tail // constant time, lists a and b share all their data
```