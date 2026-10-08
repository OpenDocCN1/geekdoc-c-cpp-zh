# 21.11 Functional Programming with LINQ Method-Call Syntax and Lambdas 909

A key aspect of functional programming is immutability—not modifying the data source being processed or any other program state, as counter-control variables in loops. Using internal iteration, you eliminate from programs common errors that are caused by modifying data incorrectly. This makes it easier to write correct code.

Filter, Map and Reduce

Three common functional-programming operations that you'll perform on collections of data are filter, map and reduce:

+   - filter operation results in a new collection containing only the elements that satisfy a condition. For example, you might filter a collection of ints to locate only the even integers, or you might filter a collection of employee's to locate only in a specific department of a large company. Filter operations do not modify the original collection.

+   - map operation results in a new collection where each element of the original collection is mapped to a new value (possibly of a different type)—e.g., mapping numeric values to the squares of the numeric values. The new collection has the same number of elements as the collection that was mapped. Map operations do not modify the original collection.

+   - reduce operation combines the elements of a collection into a single new value using a lambda that specifies how to combine the elements. For example, you might reduce a collection of 1st grades from 0 to 100 to an enum number of students with a grade greater than or equal to 60. Reduce operations do not modify the original collection.

In the next section, we'll demonstrate filter, map and reduce operations using class extension methods where Select and Aggregate, respectively. The extension methods defined by class enumerable on collections that implement the interface IEnumerable<T>.

# C# and Functional Programming

Though C# was not originally designed as a functional-programming language, C#'s query syntax and LINQ extension methods support functional-programming techniques, such as internal iteration and immutability. In addition, C# 6's getter-only, autoimplemented properties make it easier to define immutable types. We expect futures of C# and most other popular programming languages to include more functional-programming capabilities that make implementing programs with a functional style natural.

# 21.11 Functional Programming with LINQ Method-Call Syntax and Lambdas

In Chapter 9, we introduced LINQ, demonstrated LINQ query syntax and introduced some LINQ extension methods. The tasks you can perform with LINQ query syntax can also be performed with various LINQ extension methods and lambdas. In fact, the compiler translates LINQ query into calls to LINQ extension methods that receive lambdas as arguments. For example, lines 21–24 of Fig. 9.2