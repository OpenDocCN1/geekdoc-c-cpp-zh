
## 802 Chapter 15: Collection Interfaces with Standard Query Operators

```sharp
new
{
  YearOfPublication = "1877",
  Title = "Phonograph"
};
```

```sharp
var patent3 =
new
{
  patent1.Title,
  Year = patent3.YearOfPublication
};
```

```sharp
// ERROR: Cannot implicitly convert type
// 'AnonymousType#1' to 'AnonymousType#2'
//patent1 = patent2; //won't compile if uncommented
// ERROR: Cannot implicitly convert type
// 'AnonymousType#1' to 'AnonymousType#3'
//patent1 = patent3; //won't compile if uncommented
```

```sharp
// ERROR: Property or indexer 'AnonymousType#1.Title'
// cannot be assigned to -- it is read-only
//patent1.Title = "Swiss Cheese";
//won't compile if uncommented
```

The first two compile-time errors assert that the types are not compatible, so they will not successfully convert from one to the other. The third compile-time error is caused by the reassignment of the Title property. Anonymous types are immutable, so it is a compile-time error to change a property on an anonymous type once it has been instantiated.

Although not in Listing 15.28, it is not possible to declare a method with an implicit data type parameter (var). Therefore, instances of anonymous types can be passed outside the method in which they are created in only two ways. First, if the method parameter is of type object, the anonymous type instance may be passed outside the method because the anonymous type will convert implicitly. A second way is to use type inference, whereby the anonymous type instance is passed as a method type parameter that the compiler can successfully infer. Thus, calling void Method<T>(T parameter) using Function(patent1) would succeed, although the available operations on parameter within Function() are limited to those supported by object.

At the time that anonymous types were introduced, they were a breakthrough that solved an important problem: declaring a temporary type on the fly without the ceremony of having to declare a full type. Even so, they have several drawbacks, as detailed earlier. Fortunately, tuples¹² avoid these drawbacks and, in fact, essentially obviate the need for using anonymous types altogether. Specifically, tuples have the following advantages over anonymous types:

- Provide a named type that can be used anywhere a type can be used, including declarations and type parameters
- Available outside the method in which they are instantiated

One way in which tuples differ from anonymous types is that anonymous types are reference types and tuples are value types. Whether this difference is advantageous to one approach or the other depends on the performance characteristics needed. If the tuple type is frequently copied and its memory footprint is more than 128 bits, a reference type is likely preferable. Otherwise, using a tuple will most likely be more performant—and a better choice to default.

11. Starting in C# 3.0.
12. Starting in C# 7.0.

## Chapter 15: Collection Interfaces with Standard Query Operators

## ADVANCED TOPIC

### Anonymous Type Generation

Even though Console.WriteLine()'s implementation is to call ToString(), notice in Listing 15.26 that the output from Console.WriteLine() is not the default ToString(), which writes out the fully qualified data type name. Rather, the output is a list of PropertyName = value pairs, for each property on the anonymous type. This occurs because the compiler overrides ToString() in the anonymous type code generation, so as to format the ToString() output as shown. Similarly, the generated type includes overriding implementations for Equals() and GetHashCode().

The implementation of ToString() on its is an important reason that variation in the order of properties causes a new type to be generated. If two separate anonymous types, possibly in entirely separate types and even in separate namespaces, were unified and then the order of properties changed, changes in the order of properties on one implementation to ToString() have noticeable and possibly unacceptable effects on the other's results. Furthermore, at execution time, it is possible to reflect back on a type and examine the members of a type—even to call one of these members dynamically (determining at runtime which member to call). A variation in the order of members of two seemingly identical types could then trigger unexpected results. To avoid this problem, the C# designers decided to generate two different types.

## ADVANCED TOPIC

### Collection Initializers with Anonymous Types

You cannot have a collection initializer for an anonymous type, since the collection initializer requires a constructor call, and it is impossible to name the constructor. The workaround is to define a method such as static List<T>(T t) { return new List<T>(); }; Method type inference allows the type parameter to be implied rather than specified explicitly, so this workaround successfully allows for the creation of a collection of anonymous types.

Another approach to initializing a collection of anonymous types is to use an array initializer. As it is not possible to specify the data type in the constructor, array initialization syntax allows for anonymous array initializers using new[] (see Listing 15.29).

## Listing 15.29: Initializing Anonymous Type Arrays

```sharp
using System;
using System.Collections.Generic;

public class Program
{
    public static void Main()
    {
        var worldCup2006Finalists = new[]
        {
            TeamName = "France",
            Players = new string[]
            {
                "Fabian Barthez", "Gregory Coupet",
                "Mickael Landreau", "Eric Abidal",
                // ...
            },
        },
        new
        {
            TeamName = "Italy",
            Players = new string[]
            {
                "Gianluigi Buffon", "Angelo Peruzzi",
                "Marco Amelia", "Cristian Zaccardo",
                // ...
            }
        };
        Print(worldCup2006Finalists);
    }

    private static void Print<T>(IEnumerable<T> items)
{
foreach(T item in items)
{
    Console.WriteLine(item);
}
```

The resultant variable is an array of the anonymous type, which must be homogeneous.

## Summary

This chapter described the internals of how the foreach loop works and explained which interfaces are required for its execution. In addition, developers frequently filter a collection so that there are fewer items and project the collection so that the items take a different form. Toward that end, this chapter discussed the details of how to use the standard query operators—LINQ introduced collection extension methods on the System.Linq.Enumerable class—to perform collection manipulation.

In the introduction to standard query operators, we detailed the process of deferred execution and emphasized how developers should take care to avoid unintentionally re-executing an expression via a subtle call that enumerates over the collection. The deferred execution and resultant implicit execution of standard query operators is a significant factor in code efficiency, especially when the query execution is expensive. Programmers should treat the query object as the query object, not the results, and should expect the query to execute even if it executed already. The query object doesn't know the results will be the same as they were during a previous execution.

Although requirements for similar execution may be commonplace, it is not necessary to rely on standard query operators directly. Query expressions,¹³ a SQL-like syntax for manipulating collections in a way that is frequently easier to code and read, are shown in the next chapter.

The chapter ended with a detailed look at anonymous types and explained why tuples are, in fact, a preferable approach if you have C# 7.0 or later.
