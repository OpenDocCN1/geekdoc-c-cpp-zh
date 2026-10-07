
# Introducing Generic Types 635

At their core, generics offer the ability to code pattern implementations and then reuse these implementations wherever the patterns appear. Patterns describe problems that occur repeatedly within code, and templates provide a single implementation for these repeating patterns.

# Type Parameter Naming Guidelines

Just as naming a method's formal parameter, you should be as descriptive as possible when naming a type parameter. Furthermore, to distinguish the parameter as being a type parameter, its name should include a T prefix. For example, in defining a class such as EntityCollection<Entity>, you would use the type parameter name TEntity.

The only time you would not use a descriptive type name is when such a description would add any value. For example, using T in the Stack<T> class is appropriate, since the indication that T is a type parameter is sufficiently descriptive; the stack works for any type.

In the next section, you will learn about constraints. It is a good practice to use constraint-descriptive type names. For example, if a type parameter must implement IComponent, consider using a type name of TComponent.

> **Guidelines**
> DO choose meaningful names for type parameters and prefix the name with T.
> CONSIDER indicating a constraint in the name of a type parameter.

# Generic Interfaces and Structs

C# supports the use of generics throughout the language, including interfaces and structs. The syntax is identical to that used by classes. To declare an interface with a type parameter, place the type parameter in angle brackets immediately after the interface name, as shown in the example of IPair<T> in Listing 12.8.

# 636 Chapter 12: Generics

Listing 12.8: Declaring a Generic Interface

```csharp
interface IPair<T>
{
    T First { get; set; }
    T Second { get; set; }
}
```

This interface represents pairs of like objects, such as the coordinates of a point, a person’s genetic parents, or nodes of a binary tree. The type contained in the pair is the same for both items.

To implement the interface, you use the same syntax as you would for a generic class. Note that it is legal—indeed, common—for the type argument for one generic type to be a type parameter of another generic type, as shown in Listing 12.9. The type argument of the interface is the type parameter declared by the class. In addition, this example uses a struct rather than a class, demonstrating that C# supports generic value types.

Listing 12.9: Implementing a Generic Interface

```csharp
public struct Pair<T> : IPair<T>
{
    public T First { get; set; }
    public T Second { get; set; }
}
```

Support for generic interfaces is especially important for collection classes, where generics are most prevalent. Before generics were available in C#, developers relied on a series of interfaces within the System.Collections namespace. Like their implementing classes, these interfaces worked only with type object, and as a result, the interface forced all access to and from these collection classes to require a cast. By using type-safe generic interfaces, you can avoid cast operations.

# ADVANCED TOPIC

# Implementing the Same Interface Multiple Times on a Single Class

Two different constructions of the same generic interface are considered different types. Consequently, the "same" generic interface can be implemented multiple times by a class or struct. Consider the example in Listing 12.10.

Listing 12.10: Duplicating an Interface Implementation on a Single Class

```csharp
public interface IContainer<T>
{
    ICollection<T> Items { get; set; }
}
public class Person : IContainer<Address>, IContainer<Phone>, IContainer<Email>
{
    ICollection<Address> IContainer<Address>.Items {
        get
        {
            // ...
        }
        set
        {
            // ...
        }
    }
    ICollection<Phone> IContainer<Phone>.Items {
        get
        {
            // ...
        }
        set
        {
            // ...
        }
    }
    ICollection<Email> IContainer<Email>.Items {
        get
        {
            // ...
        }
    }
```

# Chapter 12: Generics

```csharp
    }
    set
      //...
    }
}
```

In this example, the Items property appears multiple times using an explicit interface implementation with a varying type parameter. Without generics, this would not be possible; instead, the compiler would allow only one explicit IContainer properties.

However, this technique of implementing multiple versions of the same interface is considered by many developers to be a "bad code smell" because it is potentially confusing (particularly if the interface permits covariant or contravariant conversions). Moreover, the Person class here seems potentially badly designed; one does not normally think of a person as being "thing that can provide a set of email addresses." When you felt to make a class implement three versions of the same interface, consider whether it might be better to make it implement three properties—for example, EmailAddresses, PhoneNumbers, and MailingAddresses—each of which returns the appropriate construction of the generic interface.

> **Guidelines**
> AVOID implementing multiple constructions of the generic interface in one type.

# Defining a Constructor and a Finalizer

Perhaps surprisingly, the constructors (and finalizer) of a generic class or struct do not require type parameters; in other words, they do not require Pair<T>(){...}. In the pair example in Listing 12.11, the constructor is declared using public Pair(T first, T second).

# Listing 12.11: Declaring a Generic Type's Constructor

```csharp
public struct Pair<T> : IPair<T>
{
    public Pair(T first, T second)
    {
        First = first;
        Second = second;
    }

    public T First { get; set; }
    public T Second { get; set; }
}
```

# Specifying a Default Value with the default operator

Listing 12.11 included a constructor that takes initial values for first and second and assigns them to First and Second. Since Pair<T> is a struct, any constructor must initialize all fields. This presents a problem, however.

Consider a constructor for Pair<T> that initializes only half, as shown in Listing 12.12, causes a error because Second is still uninitialized. If it is a nullable type, null would work, but this approach would not work if T were a non-nullable type.

# Listing 12.12: Not Initializing All Fields, causing a Compile-Time Error

```csharp
public struct Pair<T> : IPair<T>
{
    // ERROR: Field 'Pair<T>.Second' must be fully assigned
    // before control leaves the constructor
    // /
    // public Pair(T first)
    // {
    //     First = first;
    // }
    // ...
```

To deal with this scenario, C# provides the default operator. The default value of int, for example, could be specified with default. In the case of T, which Second requires, you can use default, as shown in Listing 12.13.

# Listing 12.13: Initializing a Field with the default Operator

```csharp
public struct Pair<T> : IPair<T>
{
    public Pair(T first)
    {
        First = first;
        // ...
        Second = default;
        // ...
    }
}
```

The default operator can provide the default value for any type, including type parameters.

It's possible to use default without specifying a parameter if it is possible to infer the data type. For variable initialization or assignment, use Pair<T> pair = default in place of Pair<T> pair = default(Pair<T>). Furthermore, if a method returns an int, it is possible to simply return default and the compiler infer a default(int) from the return of the method. Other scenarios where such inference is possible are default parameter (optional) values and method arguments.

Note that all nullable types have null as their default value, as nullable generic types such as default(T?). Furthermore, the default value for all reference types is null. As a result, if nullable references are enabled by C# 8.0, assigning default to a non-nullable reference type will result in a warning. Prior to C# 8.0 (and obviously after it), you should avoid assigning default or null to reference types unless null is expected to be a valid value. Where possible, favor leaving the uninitialized until a valid value is available for.
