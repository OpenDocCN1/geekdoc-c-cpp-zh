Of course, this increased flexibility comes with the same risks discussed in Section 15.6 in the context of Python:

```
Scala
val person = Noble(name = "Edmond Dantès", title = "Comte de Monte-Cristo")
printTitle(person) // prints "Comte de Monte-Cristo"
```

There is a better alternative to structural subtyping, one that has its origins in the world of functional programming: type classes. This concept appears complicated at first glance, but it is quite powerful and used extensively in functional programming libraries.

As with structural typing, the starting point is to define a type of values with a title:

```
Scala
trait Titled[A]:
  def titleOf(document: A): String
```

Titled represents a type class, the class of all types that have a title. You can then use an object of type Title[A] to display the title of a value of type A:

```
Scala
def printTitle[A](doc: A, titledEvidence: Titled[A]): Unit =
  println(titledEvidence.titleOf(doc))
```

Function printTitle takes a second argument as evidence that type A is "titled." You can apply printTitle on reports, as long as an object of type Titled[Report] is available:

```
Scala
object ReportsAreTitled extends Titled[Report]:
  def titleOf(report: Report): String = report.title

printTitle(report, ReportsAreTitled) // prints the string returned by report.title
```

Note that you can create an evidence value like ReportsAreTitled for any existing type, including one that predates function printTitle. In Scala, the evidence that a type belongs to a type class is typically passed implicitly using a context bound:

```
Scala
def printTitle[A : Titled](doc: A): Unit =
  val titledEvidence = summon[Titled[A]]
  println(titledEvidence.titleOf(doc))
```

The syntax A : Titled indicates that you must pass an implicit value of type Titled[A] to function printTitle, in addition to the document doc. This value can be retrieved