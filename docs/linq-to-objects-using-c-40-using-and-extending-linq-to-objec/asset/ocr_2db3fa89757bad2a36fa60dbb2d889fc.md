# OPTIONAL PARAMETERS AND NAMED ARGUMENTS

To demonstrate how to mix and match optional parameters and named arguments within method or constructor invocation calls, the code shown in Listing 8-3 calls the method definition for NewWay in Listing 8-2.

**Listing 8-3** Mixing and matching positional and named arguments in a method invocation for methods that have optional and mandatory arguments

```
NewWay newWay = new NewWay();

// skipping an optional parameter
newWay.DoSomething(
    "{{0},{1}} New way - param1 skipped.",
    param2: false);

// any order, but if it doesn't have a default
// it must be specified by name somewhere!
newWay.DoSomething(
    param2: false,
    formatString: "{{0},{1}} New way - params specified" +
    " by name, in any order.",
param1: 5);
```

# Using Named Arguments and Optional Parameters in LINQ Queries

Named arguments and optional parameters offer an alternative way to reduce code in LINQ, especially regarding flexibility in what parameters can be omitted in an object constructor.

Although anonymous types make it convenient to project the results of a query into an object with a subset of defined properties, these anonymous types are scoped to the local method. To share a type across methods, types, or assemblies, a concrete type is needed, meaning the accumulation of simple types or constructor methods just to hold variations of data shape projections. Object initializers reduce this need by allowing a concrete type to have a constructor without parameters and public properties used to assign values in the Select projection. Object-oriented purists take issue with a parameterless constructor being a requirement; it can lead to invalid objects being created by users who are unaware that certain