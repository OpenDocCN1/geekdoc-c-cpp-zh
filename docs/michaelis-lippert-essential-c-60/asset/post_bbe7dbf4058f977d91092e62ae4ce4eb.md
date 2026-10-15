
// Error: 'TValue': Cannot provide arguments
// when creating an instance of a variable type.
TValue newEntity = null;
// newEntity = new TValue(key);
Add(newEntity.Key, newEntity);
return newEntity;
}

One way to circumvent this restriction is to supply a factory interface that includes a method for instantiating the type. The factory implementing the interface takes responsibility for instantiating the entity rather than the EntityDictionary itself (see Listing 11.33).

## LISTING 11.33: Using a Factory Interface in Place of a Constructor Constraint

```
public class EntityBase<TKey>
{
    public EntityBase(TKey key)
    {
        Key = key;
    }
    public TKey Key { get; set; }
}

public class EntityDictionary<TKey, TValue, TFactory> :
    Dictionary<TKey, TValue>
    where TKey : IComparable<TKey>, IFormattable
    where TValue : EntityBase<TKey>
    where TFactory : IEntityFactory<TKey, TValue>, new()
{
    ...
    public TValue New(TKey key)
    {
        TFactory factory = new TFactory();
        TValue newEntity = factory.CreateNew(key);
        Add(newEntity.Key, newEntity);
        return newEntity;
    }
    ...
}

public interface IEntityFactory<TKey, TValue>
{
    TValue CreateNew(TKey key);
}
...
```

A declaration such as this allows you to pass the new key to a TValue factory method that takes parameters, rather than forcing you to rely on the
default constructor. It no longer uses the constructor constraint on TValue because TFactory is responsible for instantiating value. (One modification to the code in Listing 11.33 would be to cache a reference to the factory method—possibly leveraging Lazy<T> if multithreaded support was needed. This would enable you to reuse the factory method instead of reinstantiating it every time.)

A declaration for a variable of type EntityDictionary<TKey, TValue, TFactory> would result in an entity declaration similar to the Order entity in Listing 11.34.

## LISTING 11.34: Declaring an Entity to Be Used in EntityDictionary<...>

```
public class Order : EntityBase<Guid>
{
    public Order(Guid key) :
        base(key)
    {
        // ...
    }
}

public class OrderFactory : IEntityFactory<Guid, Order>
{
    public Order CreateNew(Guid key)
    {
        return new Order(key);
    }
}
```

## Generic Methods

Earlier, you saw that it is a relatively simple matter to add a method to a type when the type is generic; such a method can use the generic type parameters declared by the type. You did this, for example, in the generic class examples we have seen so far.

Generic methods use generic type parameters, much as generic types do. They can be declared in generic or nongeneric types. If declared in a generic type, their type parameters are distinct from those of their containing generic type. To declare a generic method, you specify the generic type parameters the same way you do for generic types: Add the type parameter declaration syntax immediately following the method name, as shown in the MathEx.Max<T> and MathEx.Min<T> examples in Listing 11.35.

### LISTING 11.36: Specifying the Type Parameter Explicitly

```
```csharp
Console.WriteLine(
    MathEx.Max<int>(7, 490));
Console.WriteLine(
    MathEx.Min<string>("R.O.U.S.", "Fireswamp"));
```
```

The output to Listing 11.36 appears in Output 11.4.

### OUTPUT 11.4

```
```text
490
Fireswamp
```
```

Not surprisingly, the type arguments, `int` and `string`, correspond to the actual types used in the generic method calls. However, specifying the type arguments is redundant because the compiler can infer the type parameters from the formal parameters passed to the method. Clearly, the caller of Max in Listing 11.36 intends the type argument to be `int` because both of the method arguments are of type `int`. To avoid redundancy, you can exclude the type parameters from the call in all cases when the compiler is able to logically infer which type arguments you must have intended. An example of this practice, which is known as **method type inference**, appears in Listing 11.37. The output appears in Output 11.5.

### LISTING 11.37: Inferring the Type Argument from the Arguments

```
```csharp
Console.WriteLine(
    MathEx.Max(7, 490)); // No type arguments!
Console.WriteLine(
    MathEx.Min("R.O.U.S.", "Fireswamp"));
```
```

### OUTPUT 11.5

```
```text
490
Fireswamp
```
```

For method type inference to succeed, the types of the arguments must be “matched” with the formal parameters of the generic method in such a way that the desired type arguments can be inferred. An interesting question to consider is what happens when contradictory inferences are made. For example, when you call the `Max<T>` method using `MathEx.Max(7.0, 490)`,
the compiler could deduce from the first argument that the type argument should be double, and it could deduce from the second argument that the type argument is int, a contradiction. In C# 2.0, this would have produced an error. A more sophisticated analysis would notice that the contradiction can be resolved because every int can be converted to double, so double is the best choice for the type argument. C# 3.0 and C# 4.0 both included improvements to the method type inferencing algorithm that permit the compiler to make these more sophisticated analyses.

In cases where method type inference is still not sophisticated enough to deduce the type arguments, you can resolve the error either by inserting casts on the arguments that clarify to the compiler the argument types that should be used in the inferences, or by giving up on type inferencing and including the type arguments explicitly.

Notice that the method type inference algorithm, when making its inferences, considers only the arguments, the arguments’ types, and the formal parameter types of the generic method. Other factors that could, in practice, be used in the analysis—such as the return type of the generic method, the type of the variable that the method’s returned value is being assigned to, or the constraints on the method’s generic type parameters—are not considered at all by the method type inference algorithm.

## Specifying Constraints

Type parameters of generic methods may be constrained in exactly the same way that type parameters of generic types are constrained. For example, you can restrict a method’s type parameter to implement an interface or to be convertible to a class type. The constraints are specified between the argument list and the method body, as shown in Listing 11.38.

## LISTING 11.38: Specifying Constraints on Generic Methods

```
public class ConsoleTreeControl
{
    // Generic method Show<T>
    public static void Show<T>(BinaryTree<T> tree, int indent)
        where T : IComparable<T>
    {
        Console.WriteLine("\n{0}{1}",
            "- ".PadLeft(5*indent, ' '),
            tree.Item.ToString());
        if (tree.SubItems.First != null)
            Show(tree.SubItems.First, indent+1);
    }
```

The problem with this code is that to the caller of the method, Deserialize<T>() appears to be type-safe. However, a cast operation is still performed on behalf of the caller, as in the case of the nongeneric equivalent shown here:

```
string greeting =
    (string)Deserialization.Deserialize(stream, formatter);
```

The cast could fail at runtime; the method might not be as type-safe as it appears. The Deserialize<T> method is generic solely so that it can hide the existence of the cast from the caller, which seems dangerously deceptive. It might be better for the method to be nongeneric and return object, making the caller aware that it is not type-safe. Developers should use care when casting in generic methods if there are no constraints to verify cast validity.

## Guidelines

AVOID misleading the caller with generic methods that are not as type-safe as they appear.

## Covariance and Contravariance

A question often asked by new users of generic types is why an expression of type List<string> may not be assigned to a variable of type List<object>—if a string may be converted to type object, surely a list of strings is similarly compatible with a list of objects. But this is not, generally speaking, either type-safe or legal. If you declare two variables with different type parameters using the same generic class, the variables are not type-compatible even if they are assigning from a more specific type to a more generic type—in other words, they are not covariant.

Covariant is a technical term from category theory, but its underlying idea is straightforward: Suppose two types X and Y have a special relationship—namely, that every value of the type X may be converted to the type Y. If the types I<X> and I<Y> always also have that same special relationship, we say, “I<T> is covariant in T.” When dealing with simple generic types with only one type parameter, the type parameter can be understood and we simply say, “I<T> is covariant.” The conversion from I<X> to I<Y> is called a covariant conversion.
