Type Length is implemented as a double value but is incompatible with type Double. Outside the defining package, you cannot call wholeMeters on a Double value.

Kotlin achieves the same type safety using inline classes (which was the approach used in earlier versions of Scala):

```
@JvmInline
value class Length(val meters: Double)

fun fromMeters(meters: Double): Length = Length(meters)
fun wholeMeters(len: Length): Length = Length(ceil(len.meters))
```

As in Scala, wholeMeters cannot be called on a Double value. However, because Length is an inline class, wholeMeters is implemented internally as a function from Double to Double and does not involve the construction of objects of type Length at runtime. Thus, it delivers type safety without a runtime cost, as in Scala. Some standard library types, such as Result used earlier, are defined in terms of value classes for improved performance.

Java and Kotlin differ noticeably in regard to type variance. The case of Java was discussed in Section 15.8. By contrast, Kotlin is much closer to Scala. Most Book/Magazine/Publication examples from Chapter 15 could be written in Kotlin:

```
fun printTitles(pubs: List<Publication>) {
    for (pub in pubs) println(pub.title)
}

val books: List<Book> = listOf(book1, book2)
printTitles(books) // prints both titles
```

This code successfully prints the titles of both books. Recall that a similar printTitles function in Java could not be invoked on a List<Book> value because lists are non-variant in Java. In Kotlin, the List type is covariant. It is defined as follows:

```
public interface List<out E> : Collection<E> { ... }
```

The variance annotation out plays the same role as “+” in Scala and makes the immutable List type covariant. As in Scala, mutable types are non-variant. Types such as Array and MutableList are defined in this way

```
public class Array<T> { ... }
public interface MutableList<E> : List<E>, MutableCollection<E> { ... }
```