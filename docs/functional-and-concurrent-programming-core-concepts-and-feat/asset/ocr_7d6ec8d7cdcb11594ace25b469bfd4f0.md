A shorted syntax _.title is used to define given values. Since Titled is a SAM interface, you can use a function to define a Titled object and thus rely on partial application or lambda expressions.

When you define type classes, you rely on ad hoc polymorphism—various titleOf methods with distinct signatures—instead of subtype polymorphism—the same title method implemented differently in separate subtypes. This improves flexibility because existing types can easily be added to a type class without modification: The necessary code, like method titleOf, resides outside the type.

For instance, this definition of method printTitlesInOrder is preferable to that of Listing 15.10, which uses a Publication & Ordered[A] bound:

```
def printTitlesInOrder[A <: Publication : Ordering](pubs: Set[A]): Unit =
  for pub <- SortedSet.from(pubs) do println(pub.title)
```

Listing 15.14: Example of combining type bounds and type classes for flexibility.

This variant of the function is more flexible because you can use it on any publication type A for which an Ordering[A] value is defined, including publication types that are not subtypes of Ordered. For instance, thanks to implicit conversions from the standard library, printTitlesInOrder can now be called on publications that extend Java’s Comparable interface.

There are several benefits to using type classes instead of structural types. First, an attempt to print the title of a noble person is now rejected:

```
no implicit argument of type Titled[Noble] was found for an implicit parameter of method printTitle
```

Second, you can use printTitles on documents that conceptually have a title but define no title method. You simply need to create a suitable evidence object:

```
case class Memo(header: String)
val memo = Memo("Famous Counts")

given Titled[Memo] = _.header

printTitle(memo) // prints "Famous Counts"
```

Even though memos have headers instead of titles, you can call printTitle on memos.

Third, values and methods can be associated with each type class:

```
trait Titled[A]:
  def titleOf(document: A): String
  def logger: Logger = Logger.getAnonymousLogger
```