# B.3.3 implicit Parameters

It is possible to get Scala to implicitly pass extra parameters into a method as well. This can be done for multiple reasons, including passing implicit type conversions. Scala will only implicitly include the last argument list to a method or function. Typically, methods that have implicit parameters are curried. For the last parameter list to be supplied implicitly the argument list must be labeled as implicit and there must be a value matching each of the types in that parameter list which is in scope and labeled as implicit. Note that this implies that you can make implicit val declarations as well as implicit def declarations.

If you look in the Application Programming Interface (API), for example at scala.collection.Seq, you will see many examples of methods that include implicit parameters. In the collections library the implicit parameter list is almost always a single parameter of the type CanBuildFrom.

# B.3.4 The Meaning of <%

When you put <% as a bound on a type parameter, Scala switches it to a normal type bound and adds a curried implicit parameter to the method. That extra parameter will be filled in with an appropriate implicit conversion from the current scope if one is available.

# B.4 sealed classes

Many functional languages have a construct called algebraic types. This allows you to say that a type can be represented by a small number of different possible structures/values. If all you want are separate values, the Enumeration described above is the way to go. When the different possibilities have different structure to them, the normal object-oriented way to represent that is with inheritance. The one shortcoming of inheritance in this case is that anyone can add other subtypes at a later date, and that might be a problem. If you make a class final, no subtypes are allowed. In this case you want to be able to limit the subtypes to a specific number.

This mechanism is provided in Scala with the sealed keyword. A sealed class can be extended, but all the subtypes have to appear in the same file as the original declaration. That gives you much stronger control over what subtypes exist.

There is another benefit to a class being sealed in the form of error checking for match expressions. If you do a match on an expression whose type is a sealed class, Scala will produce syntax errors if you do not have cases that can match all subtypes. This completeness checking makes it so that you should not get MatchExceptions when a type comes in that you were not expecting.

The standard usage of a sealed class is to use a sealed abstract class that is completely empty at the top of the hierarchy, then have various case classes or case