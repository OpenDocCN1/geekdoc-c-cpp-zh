
Here, the `Show<>` implementation itself does not directly use any member of the `IComparable<>` interface, so you might wonder why the constraint is required. Recall, however, that the `BinaryTree<>` class did require this constraint (see Listing 12.39).

### LISTING 12.39: BinaryTree<> Requiring IComparable<> Type Parameters

```csharp
public class BinaryTree<>
where T: System.IComparable<>
{
...
}
```

Because the `BinaryTree<>` class requires this constraint on its T, and because `Show<>` uses its T as a type argument corresponding to a constrained type parameter, `Show<>` needs to ensure that the constraint on the class's type parameter is met on its method type argument.

## ADVANCED TOPIC

## Casting inside a Generic Method

Sometimes you should be wary of using generics—for instance, when using them specifically to bury a cast operation. Consider the following method, which converts a stream into an object of a given type:

```csharp
public static T Deserialize<>(
    Stream stream, IFormatter formatter)
{
    return (T)formatter.Deserialize(stream);
}
```

The formatter is responsible for removing data from the stream and converting it to an object. The `Deserialize()` call on the formatter returns data of type `object`. A call to use the generic version of `Deserialize()` looks something like this:

```csharp
string greeting =
    Deserialization.Deserialize<>(stream, formatter);
```

The problem with this code is that to the caller of the method, `Deserialize<>()` appears to be type-safe. However, a cast operation is still performed on behalf of the caller, as in the case of the nongeneric equivalent shown here:

```csharp
string greeting =
    (string)Deserialization.Deserialize(stream, formatter);
```

The cast could fail at runtime; the method might not be as type-safe as it appears. The `Deserialize<T>` method is generic solely so that it can hide the existence of the cast from the caller, which seems dangerously deceptive. It might be better for the method to be nongeneric and return `object`, making the caller aware that it is not type-safe. Developers should use care when casting in generic methods if there are no constraints to verify cast validity.

## Guidelines

AVOID misleading the caller with generic methods that are not as type-safe as they appear.

## Covariance and Contravariance

A question often asked by new users of generic types is why an expression of type `List<string>` may not be assigned to a variable of type `List<object>`—if a `string` may be converted to type `object`, surely a list of strings is similarly compatible with a list of objects. But this is not, generally speaking, either type-safe or legal. If you declare two variables with different type parameters using the same generic class, the variables are not type-compatible even if they are assigning from a more specific type to a more generic type—in other words, they are not covariant.

Covariant is a technical term from category theory, but its underlying idea is straightforward: Suppose two types X and Y have a special relationship—namely, that every value of the type X may be converted to the type Y. If the types `I<X>` and `I<Y>` always also have that same special relationship, we say, “`I<T>` is covariant in T.” When dealing with simple generic types with only one type parameter, the type parameter can be understood and we simply say, “`I<T>` is covariant.” The conversion from `I<X>` to `I<Y>` is called a covariant conversion.

For example, instances of a generic class, `Pair<Contact>` and `Pair<PdaItem>`, are not type-compatible even when the type arguments are themselves compatible. In other words, the compiler prevents the conversion (implicit or explicit) of `Pair<Contact>` to `Pair<PdaItem>`, even though `Contact` derives from `PdaItem`. Similarly, converting `Pair<Contact>` to the interface type `IPair<PdaItem>` will also fail. See Listing 12.40 for an example.

### LISTING 12.40: Conversion between Generics with Different Type Parameters

```csharp
// ...
// Error: Cannot convert type ...
Pair<PdaItem> pair = (Pair<PdaItem>) new Pair<Contact>();
IPair<PdaItem> duple = (IPair<PdaItem>) new Pair<Contact>();
```

But why is this not legal? Why are `List<T>` and `Pair<T>` not covariant? Listing 12.41 shows what would happen if the C# language allowed unrestricted generic covariance.

### LISTING 12.41: Preventing Covariance Maintains Homogeneity

```csharp
//...
Contact contact1 = new Contact("Princess Buttercup"),
Contact contact2 = new Contact("Inigo Montoya");
Pair<Contact> contacts = new Pair<Contact>(contact1, contact2);

// This gives an error: Cannot convert type ...,
// but suppose it did not
// IPair<PdaItem> pdaPair = (IPair<PdaItem>) contacts;
// This is perfectly legal but not type-safe
// pdaPair.First = new Address("123 Sesame Street");
...
```

An `IPair<PdaItem>` can contain an address, but the object is really a `Pair<Contact>` that can contain only contacts, not addresses. Type safety is completely violated if unrestricted generic covariance is allowed. Now it should also be clear why a list of strings may not be used as a list of objects. You cannot insert an integer into a list of strings, but you can insert an integer into a list of objects; thus it must be illegal to cast a list of strings to a list of objects, an error the compiler can enforce.

## Enabling Covariance with the out Type Parameter Modifier in C# 4.0 (and Later)

You might have noticed that both problems described earlier as consequences of unrestricted covariance arise because the generic pair and the generic list allow their contents to be written. Suppose we eliminated this possibility by making a read-only `IReadOnlyPair<T>` interface that exposes T only as coming “out” of the interface (i.e., used as the return type of a method or read-only property) and never going “into” it (i.e., used as a formal parameter or writeable property type). If we restricted ourselves to an “out only” interface with respect to T, the covariance problem just described would not occur (see Listing 12.42).

### LISTING 12.42: Potentially Possible Covariance

```csharp
interface IReadOnlyPair<T>
{
  T First { get; }
  T Second { get; }
}

interface IPair<T>
{
  T First { get; set; }
  T Second { get; set; }
}

public struct Pair<T> : IPair<T>, IReadOnlyPair<T>
{
  // ...
}

class Program
{
  static void Main()
  {
    // Error: Only theoretically possible without
    // the out type parameter modifier
    Pair<Contact> contacts =
      new Pair<Contact>(
        new Contact("Princess Buttercup"),
        new Contact("Inigo Montoya") );
    IReadOnlyPair<PdaItem> pair = contacts;
    PdaItem pdaItem1 = pair.First;
    PdaItem pdaItem2 = pair.Second;
  }
}
```

When we restrict the generic type declaration to expose data only as it comes out of the interface, there is no reason for the compiler to prevent covariance. All operations on an `IReadOnlyPair<PdaItem>` instance would convert Contacts (from the original `Pair<Contact>` object) up to the base class `PdaItem`—a perfectly valid conversion. There is no way to “write” an address into the object that is really a pair of contacts, because the interface does not expose any writable properties.

The code in Listing 12.42 still does not compile. However, support for safe covariance was added to C# 4. To indicate that a generic interface is intended to be covariant in one of its type parameters, you can declare the type parameter with the `out` type parameter modifier. Listing 12.43 shows how to modify the interface declaration to indicate that it should be allowed to be covariant.

### LISTING 12.43: Covariance Using the out Type Parameter Modifier

```csharp
  ...
interface IReadOnlyPair<out T>
{
  T First { get; }
  T Second { get; }
}
```

Modifying the type parameter on the `IReadOnlyPair<out T>` interface with `out` will cause the compiler to verify that T is, indeed, used only for “outputs”—method return types and read-only property return types—and never for formal parameters or property setters. From then on, the compiler will allow any covariant conversions involving the interface to succeed. When this modification is made to the code in Listing 12.42, it will compile and execute successfully.

Several important restrictions are placed on covariant conversions:

-   Only generic interfaces and generic delegates (described in Chapter 13) may be covariant. Generic classes and structs are never covariant.

-   The varying type arguments of both the source and target generic types must be reference types, not value types. That is, an `IReadOnlyPair<string>` may be converted covariantly to `IReadOnlyPair<object>` because both `string` and `IReadOnlyPair<object>` are reference types. An `IReadOnlyPair<int>` may not be converted to `IReadOnlyPair<object>` because `int` is not a reference type.

![](img/ef6a8a417630b222bfb3f3b949facff0_563_0.png)

![](img/ef6a8a417630b222bfb3f3b949facff0_563_1.png)
