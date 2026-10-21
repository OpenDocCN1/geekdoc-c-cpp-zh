
Java and Kotlin offer bridges between methods and functions via method references. Kotlin also defines a shorter form for anonymous functions, where x -> f(x) is replaced with f(it), similar to Scala’s use of “_” for partial application:

```
Kotlin
fun pos(x: Int): Boolean = x > 0

val neg: (Int) -> Boolean = negate { x -> pos(x) }
val neg: (Int) -> Boolean = negate { pos(it) }
val neg: (Int) -> Boolean = negate(::pos)
```

If pos were a method of an object ref, you would replace ::pos with ref::pos in the last expression. In Java, methods are always defined within a class, so the “::” operator used for method reference always has a left-hand-side argument:

```
Java
class Math {
    public boolean pos(int x) {
        return x > 0;
    }
}
Math m = new Math();

Predicate<Integer> neg = negate(x -> m.pos(x));
Predicate<Integer> neg = negate(m::pos);
```

In the other direction, lambda expressions can be used to implement methods. In Java, like in Scala, lambda expressions can implement SAM interfaces directly:

```
Scala
val byLength: Comparator[String] = (a, b) => a.length.compareTo(b.length)
```

```
Java
Comparator<String> byLength = (a, b) -> Integer.compare(a.length(), b.length());
```

By contrast, in Kotlin, you often need to mention an interface’s name explicitly for a lambda expression to implement it:

```
Kotlin
// rejected by the compiler:
val byLength: Comparator<String> = { a, b -> a.length.compareTo(b.length) }

val byLength = Comparator<String> { a, b -> a.length.compareTo(b.length) } // OK
```

In Java, lambda expressions actually require that you use a SAM interface:

```
Java
ToIntFunction<String> len = (String str) -> str.length(); // OK
Object len = (String str) -> str.length(); // rejected by the compiler
var len = (String str) -> str.length();    // rejected by the compiler
```

This is not an issue in Scala or Kotlin:

```
Scala
val len: Any = (str: String) => str.length // OK
val len = (str: String) => str.length      // type String => Int inferred
```

```
Kotlin
val len: Any = { str: String -> str.length } // OK
val len = { str: String -> str.length }      // type (String) -> Int inferred
```

Recall that, in Scala, functions can be curried, and single-argument calls can use curly braces instead of parentheses:

```
Scala
def existsOrEmpty[A](list: List[A])(test: A => Boolean): Boolean =
    list.isEmpty || list.exists(test)

val e = existsOrEmpty(List(1, 2, 3)) { num =>
    num > 1
}
```

Kotlin has no curried functions but uses a different “trick” for the same purpose. It lets you move a lambda expression—which includes its own pair of braces—outside the list of arguments if it is the last argument in a call:

```
Kotlin
fun <A> existsOrEmpty(list: List<A>, test: (A) -> Boolean): Boolean =
    list.isEmpty() || list.any(test)

val e = existsOrEmpty(listOf(1, 2, 3)) { num ->
    num > 1
}
```

Notice how, in the last expression, the lambda expression { num -> num > 1 } has been moved outside the list of existsOrEmpty arguments.

Kotlin's any, used in the preceding example, is equivalent to the Scala method exists. Kotlin collections define most standard higher-order functions, including forEach, filter, map, and flatMap. For instance, you can convert Fahrenheit temperatures into Celsius using map:

```
temps.map { temp -> ((temp - 32) / 1.8f).roundToInt() }
```

As a more complex combination of higher-order functions, you could start from a list of strings, parse each string as a space-separated list of temperatures, ignore non-numerical values, and convert numerical values to Celsius:

```
val SPACES = Regex("\\s+")
val strings: List<String> = ...

val celsius: List<Int> = strings
    .flatMap { SPACES.split(it) }
    .mapNotNull { it.toIntOrNull() }
    .map { ((it - 32) / 1.8f).roundToInt() }
```

This example uses the shorter syntax based on it. Kotlin tends to use null where Scala would use options—for instance, toIntOrNull instead of toIntOption. Method mapNotNull combines a mapping and filtering steps, ignoring null outputs of the mapped function.

In Java, the standard collections implement very few higher-order functions. Instead, collections are bridged into streams, which implement all the higher-order functions. A simple conversion into Celsius could be written as follows:

```
List<Integer> temps = ...

List<Integer> celsius = temps.stream().map(temp -> round((temp - 32) / 1.8f)).toList();
```

This calculation forces boxing and unboxing of primitive int values to and from Integer values. To avoid it, Java also defines specialized stream classes for its primitive types:

```
int[] temps = ...

int[] celsius = Arrays.stream(temps).map(temp -> round((temp - 32) / 1.8f)).toArray();
```

In this computation, map is invoked on an object of type IntStream instead of Stream.

You can also implement in Java the more complex transformation shown earlier, from a list of lines into a list of Celsius temperatures. There is no standard Java function to parse a string into an optional integer (or even into a nullable integer), so you need to write one first:

```
Optional<Integer> parse(String str) {
    try {
        return Optional.of(Integer.valueOf(str));
    } catch (NumberFormatException ex) {
        return Optional.empty();
    }
}
```

Using this function, the code for the transformation is similar to what it would be in Scala. The key difference is that an option needs to be converted into a stream explicitly in the second call to flatMap (Scala uses an implicit conversion there):

```
Pattern SPACES = Pattern.compile("\\s+");
List<String> strings = ...

List<Integer> celsius = strings.stream()
    .flatMap(str -> Arrays.stream(SPACES.split(str)))
    .flatMap(str -> parse(str).stream())
    .map(temp -> round((temp - 32) / 1.8f))
    .toList();
```

You could also write a variant that processes an array of strings String[] into an array of integers int[] by using OptionalInt instead of Optional and IntStream instead of Stream.

When higher-order functions return functions, closures are created in both Java and Kotlin. The memoization example of Listing 12.2 can be written in either language:

```
<A, B> Function<A, B> memo(Function<A, B> f) {
    Map<A, B> store = new HashMap<>();
    return x -> store.computeIfAbsent(x, f);
}
```

```
fun <A, B> memo(f: (A) -> B): (A) -> B {
    val store = mutableMapOf<A, B>()
    return { x -> store.computeIfAbsent(x, f) }
}
```

In Kotlin, closures can write the captured data, as they do in Scala:

```
fun <A, B> single(f: (A) -> B): (A) -> B {
    var called = false
    return { x ->
        if (called) throw IllegalStateException()
        called = true
        f(x)
    }
}
```

This example creates a variant of a function f that can be invoked only once before it throws an exception—for instance, for the purpose of testing. This requires writing the Boolean variable called from the closure. By contrast, Java does not allow closures to reassign variables. This code is rejected by the compiler:

```
<A, B> Function<A, B> single(Function<A, B> f) {
    var called = false;
    return x -> {
        if (called) throw new IllegalStateException();
        called = true; // rejected at compile time
        return f.apply(x);
    };
}
```

Instead, you can replace the lambda expression with an anonymous class that defines a reassignable Boolean field:

```
<A, B> Function<A, B> single(Function<A, B> f) {
    return new Function<>() {
        private boolean called = false;

        public B apply(A x) {
            if (called) throw new IllegalStateException();
            called = true;
            return f.apply(x);
        }
    };
}
```

The argument f is still captured in a closure, but it is only read and not reassigned.

## A.6 Lazy Evaluation

By replacing values with no-argument functions (thunks), you can delay the evaluation of function arguments in both Java and Kotlin. The fancier by-name arguments of Scala do not exist in either language.

Kotlin, however, makes the arrow of a lambda expression optional when the lambda takes no arguments or its arguments are ignored. The following Scala expressions

```
Scala
List.tabulate(5)(i => "X" * (i + 1)) // [X, XX, XXX, XXXX, XXXXX]
List.fill(5)(Random.between(1, 11)) // 5 numbers, possibly different
```

can be written in Kotlin as

```
Kotlin
List(5) { i -> "X".repeat(i + 1) }
List(5) { Random.nextInt(1, 11) }
```

You can use the same function List where you need two functions, tabulate and fill, in Scala. The Kotlin function used in this example is equivalent to tabulate. You could write the last line in the preceding example as

```
Kotlin
List(5) { _ -> Random.nextInt(1, 11) }
```

but the unused argument and arrow are optional.

This makes it possible to achieve in Kotlin a form of control abstraction similar to Scala’s, despite the lack of by-name arguments. For instance, you can rewrite function timeOf from Listing 12.3 in this way:

```
Kotlin
fun <U> timeOf(code: () -> U): Double {
    val start = System.nanoTime()
    code()
    val end = System.nanoTime()
    return (end - start) / 1E9
}
```

It is used in exactly the same way as the Scala variant, with no explicit thunk visible:
