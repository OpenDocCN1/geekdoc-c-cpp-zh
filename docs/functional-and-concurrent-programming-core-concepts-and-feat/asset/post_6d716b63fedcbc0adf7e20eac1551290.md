
![](img/74309e2bdd93f68d2e94338a3d73517f_278_0.png)

## Figure 15.1 Subtype relationship of two functions.

and functions are covariant in their output type. Indeed, if you have a higher-order function defined as

```
Scala
def higherOrder(f: Book => Publication) = ...
```

you can safely call it on an argument of type Publication => Magazine. As a function, this argument can be applied to values of type Book (it can be applied to any publication type) and will produce values of type Publication (specifically, magazines), so it is consistent with the type requirements of argument f.

Peculiarities might arise when variance is considered. Here are two examples. First, immutable sets in Scala are non-variant. The reason is that Set[A] is a subtype of A => Boolean. The data structure view calls for covariance, but the function type would require contravariance.

Second, while all other data structures are non-variant in Java, arrays are covariant. This design choice predates the introduction of generics and was necessary to improve flexibility. For instance, you can define a sorting function with signature Object[] and apply it to a String[] value—String[] is a subtype of Object[]. Since arrays are mutable, however, this covariance leads to type unsoundness:

```
Java
void printTitlesAndAddMagazine(Publication[] pubs) {
    for (Publication pub : pubs) System.out.println(pub.title());
    pubs[0] = new Magazine(...);
}

Book[] books = new Book[]{book1, book2};
printTitlesAndAddMagazine(books); // throws ArrayStoreException
```

The type system allows the invocation of function printTitlesAndAddMagazine on an array of books, but an attempt to insert a magazine into the array results in a runtime exception. The situation is the same in C#, where arrays are also covariant and may trigger an ArrayTypeMismatchException. Arrays are non-variant in Scala and Kotlin.

You can use “<:” to specify an upper bound, meaning that you require a type variable to be a subtype of another type. You can use the opposite operator “>:” to specify a lower bound, requiring a type variable to be a supertype of another type:

```
```scala
def addMagazine[A >: Magazine](pubs: Set[A]): Unit = pubs += Magazine(...)
```
```

Listing 15.8: Example of a lower type bound for use-site variance.

Function `addMagazine` adds a magazine to a mutable set, requiring type `A` to be a supertype of `Magazine`. The function is flexible, and you can call it on values of type `Set[Magazine]`, `Set[Publication]`, or `Set[AnyRef]`.

When you use type bounds, you face constraints similar to what we saw earlier with covariant and contravariant types. For instance, these functions are rejected by the compiler:

```
```scala
def printTitlesAndAddMagazine[A <: Publication](pubs: Set[A]): Unit =
  for pub <- pubs do println(pub.title)
  pubs += Magazine(...) // rejected by the compiler

def printTitlesAndAddMagazine[A >: Magazine](pubs: Set[A]): Unit =
  for pub <- pubs do println(pub.title) // rejected by the compiler
  pubs += Magazine(...)
```
```

The first function is rejected because it attempts to add a magazine to a `Set[A]` value, but all you know is that type `A` is a subtype of `Publication`. There is no guarantee that type `A` is a supertype of type `Magazine`—it could be `Book`, for instance. The second function fails because it tries to invoke a `title` method on a value of type `A`, but `A` is only known to be a supertype of `Magazine`, not necessarily a subtype of `Publication`—type `A` could be `AnyRef`, for instance. To make it work, `printTitlesAndAddMagazine` needs `A` to be both a subtype of `Publication` and a supertype of `Magazine`. You implement it by specifying both a lower bound and an upper bound:

```
```scala
def printTitlesAndAddMagazine[A >: Magazine <: Publication](pubs: Set[A]): Unit =
  for pub <- pubs do println(pub.title)
  pubs += Magazine(...)
```
```

Listing 15.9: Example of a type parameter with both lower and upper bounds.

In more complex scenarios, you can combine type bounds with type intersections to specify multiple upper or lower bounds:

```
def printTitlesInOrder[A <: Publication & Ordered[A]](pubs: Set[A]): Unit =
  for pub <- SortedSet.from(pubs) do println(pub.title)
```

Listing 15.10: Example of a combined upper type bound; contrast with Lis. 15.14.

Publications can be gathered in a sorted set because type A is known to be an ordered type, in addition to being a subtype of Publication.

Most of the functions used as illustrations in this section can be written in Java:

```
<A extends Publication> void printTitles(Set<A> pubs) {
  for (Publication pub : pubs) System.out.println(pub.title());
}

void addMagazine(Set<? super Magazine> pubs) {
  pubs.add(new Magazine(...));
}

<A extends Publication & Comparable<A>> void printTitlesInOrder(Set<A> pubs) {
  for (Publication pub : new TreeSet<>(pubs)) System.out.println(pub.title());
}
```

Java uses S extends T and ? extends T to express upper bounds and ? super T to express lower bounds. Java has no S super T syntax, making it necessary to use a wildcard in the definition of function addMagazine. As of this writing, lower bounds and upper bounds cannot be combined in Java, preventing you from writing an equivalent to function printTitlesAndAddMagazine from Listing 15.9.

When designing libraries that depend on non-variant types, it is good practice to rely on type bounds for increased flexibility. Consider, for instance, a function that executes tasks in parallel and returns a list of their outputs. 11 Tasks are specified as no-argument functions:

```
public <A> List<A> runInParallel(List<Function0<A>> tasks) {...}
```

Because lists are non-variant in Java, a limitation of runInParallel is that it cannot be invoked on a value of type List<T> where T is a subtype of Function0<Book>. For instance, suppose BookPublisher is a book-generating function:

```
class BookPublisher implements Function0<Book> { ... }
```

11 See the case study in Chapter 24 for a possible implementation strategy.

You cannot invoke runInParallel on a List<BookPublisher>. Adding a type bound can make the function more flexible:

```
public <A> List<A> runInParallel(List<? extends Function0<A>> tasks) {...}
```

You can now call this function on a List<BookPublisher>. However, it then returns a value of type List<Book> specifically:

```
List<BookPublisher> bookPublishers = ...
List<Book> books = runInParallel(bookPublishers); // OK
List<Publication> pubs = runInParallel(bookPublishers); // rejected by the compiler
```

For the last line to work, type A would have to be Publication. But BookPublisher is a subtype of Function0<Book>, not a subtype of Function0<Publication>, and function types are not covariant in Java: Function0<Book> is not a subtype of Function0<Publication>.

You can further improve the runInParallel function by using a second type bound, inside the function type:

```
public <A> List<A> runInParallel(List<? extends Function0<? extends A>> tasks) {...}
```

Listing 15.11: Using type bounds on non-variant types for increased flexibility.

This second bound makes it possible to call runInParallel(bookPublishers) and have the return value be of type List<Publication> because BookPublisher is a subtype of Function0<? extends Publication>. You can define a similar function in Scala:¹²

```
def runInParallel[A](tasks: List[() => A]): List[A] = ...

val bookPublishers: List[BookPublisher] = ...
val pubs: List[Publication] = runInParallel(bookPublishers) // OK
```

The definition is simpler and needs no type bounds because, in Scala, lists are covariant and functions are also covariant in their return type. Type A can be Publication because BookPublisher is a subtype of () => Book, and () => Book is a subtype of () => Publication.

¹²An even more flexible function would use kinds (higher-order types) so a list is returned from a list, a set from a set, etc.
