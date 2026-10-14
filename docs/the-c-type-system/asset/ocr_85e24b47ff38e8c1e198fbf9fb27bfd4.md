# Parametric Polymorphism with Generics

C# generics offer parametric polymorphism, a form of polymorphism that allows us to write code once that works for multiple types by using generic type parameters instead of actual types. This approach provides a common form and purpose for all the types that can be substituted for those parameters.

This is most clearly demonstrated by the generic collection classes in the Standard Library, such as List<T>, where T is a generic parameter type that can be substituted by any run-time type, including any types we define ourselves. For example, in Listing 7-19 we declare two List<T> variables parameterized with different, unrelated types.

```
var colors = new List<Color>();
var names = new List<string>();
```

Listing 7-19: Using a generic type

Although the List implementation’s behavior doesn’t change, a List<Color> is a distinct type from List<string>, and there’s no relationship between the two types. The generic List<T> code is written in terms of the T generic parameter, and since List<T> doesn’t need to know anything about the structural or behavioral characteristics of T, it can be used with any type.

To put that another way, in the context of List<T>, any type can be substituted for the T parameter without implying any subtype relationship. We have no behavioral contract to take into account, because List<T> makes no assumptions about T.

If we need to be more selective about the types that are suitable for a generic parameter type in our own generic code, or if we require the generic code to use methods and properties beyond those provided by object, we can constrain the parameter to allow only types having specific behavior.

# Generic Constraints and Protocol Interfaces

Since object is the base class of every type, generics can use its methods via a variable of type T, but to access anything else, the compiler needs more information on what T can be. We provide that information through generic type constraints. One example is an interface constraint, which restricts T to a type that implements the specified interface, ensuring that all interface operations are legal for a variable of that generic type. Consider, for instance, the interface shown in Listing 7-20.

```
public interface IParser<T>
{
    public T Parse(string input);
}
```

Listing 7-20: A contract interface