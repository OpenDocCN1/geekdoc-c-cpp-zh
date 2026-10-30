Additionally, whenever a method or property of the `NullUser` object is expected to return a reference to another object, it should return a special Null Object implementation of *those* types, too. In other words, all Null Object implementations should return recursive Null Object implementations. This removes the need for any null reference checking in clients.

This also has the added benefit of reducing the number of unit tests that you need to write. Previously, when each client had to implement the check, there would also be concomitant unit tests to confirm that the check was in place. Instead, the repository implementation is unit tested to ensure that it returns the `NullUser` implementation.

> ### Cascading nulls
> 
> C# 6 introduced a *cascading nulls operator*, also called the *null-conditional operator* and the *safe navigation operator*. This allows the following code snippet to be simplified from this:
> 
> ```csharp
> if(person != null && person.Details != null && person.Detail.Age > 30)
> {
>     // . . .
> }
> ```
> 
> To this:
> 
> ```csharp
> if(person?.Details?.Age > 30)
> {
>     // . . .
> }
> ```

The `?.` operator thus becomes a way of safely dereferencing any object and, at worst, being handed a default(T) of the property type. This has proven to be a useful addition to the language, but I am reluctant to use this as an alternative to a proper Null Object implementation, for a couple of reasons.

First, there are too many instances in which a default value of a type is simply not going to suffice. The previous example of using a sensible user name to avoid throwing a NullReferenceException illustrates that the alternative is not a default value but something more meaningful to the application.

Second, the null coalescing requires all clients of the code to be programmed with the possibility of null in mind. Part of the reason to use the Null Object pattern is to obviate null checking and give you the freedom to dereference with impunity. If you reject the Null Object pattern in favor of the Cascading Nulls syntax, you open yourself up to forgetting to dereference again.

Given a proper Null Object implementation, this example could be written succinctly as shown here.

```
```csharp
if(person.Details.Age > 30)
{
    // . . .
}
```
```

This, surely, offers the most benefit: client code that is less obfuscated but that is safe from the perils of a NullReferenceException.