
constraint to T. If nullable value types satisfied that constraint, it would be possible to define the nonsense type Nullable<Nullable<int>>. A doubly nullable integer is confusing to the point of being meaningless. (As expected, the shorthand syntax int?? is also disallowed.)

## Multiple Constraints

For any given type parameter, you may specify any number of interface type constraints, but no more than one class type constraint (just as a class may implement any number of interfaces but inherit from only one other class). Each new constraint is declared in a comma-delimited list following the generic type parameter and a colon. If there is more than one type parameter, each must be preceded by the `where` keyword. In Listing 12.25, the generic `EntityDictionary` class declares two type parameters: `TKey` and `TValue`. The `TKey` type parameter has two interface type constraints, and the `TValue` type parameter has one class type constraint.

### LISTING 12.25: Specifying Multiple Constraints

```csharp
public class EntityDictionary<TKey, TValue>
    : Dictionary<TKey, TValue>
    where TKey : IComparable<TKey>, IFormattable
    where TValue : EntityBase
{
...
}
```

In this case, there are multiple constraints on `TKey` itself and an additional constraint on `TValue`. When specifying multiple constraints on one type parameter, an AND relationship is assumed. If a type C is supplied as the type argument for `TKey`, C must implement `IComparable<C>` and `IFormattable`, for example.

Notice there is no comma between each `where` clause.

## Constructor Constraints

In some cases, it is desirable to create an instance of the type argument's type inside the generic class. In Listing 12.26, for example, the `MakeValue()` method for the `EntityDictionary<TKey, TValue>` class must create an instance of the type argument corresponding to type parameter `TValue`.

### LISTING 12.26: Requiring a Default Constructor Constraint

```csharp
public class EntityBase<TKey>
{
    public TKey Key { get; set; }
}

public class EntityDictionary<TKey, TValue>
    : Dictionary<TKey, TValue>
    where TKey : IComparable<TKey>, IFormattable
    where TValue : EntityBase<TKey>, new()
{
    // ...
    public TValue MakeValue(TKey key)
    {
        TValue newEntity = new TValue();
        newEntity.Key = key;
        Add(newEntity.Key, newEntity);
        return newEntity;
    }
    // ...
}
```

Because not all objects are guaranteed to have public default constructors, the compiler does not allow you to call the default constructor on an unconstrained type parameter. To override this compiler restriction, you can add the text `new()` after all other constraints are specified. This text is a constructor constraint, and it requires the type argument corresponding to the constrained type parameter to have a public default constructor. Only the default constructor constraint is available. You cannot specify a constraint that ensures that the type argument supplied provides a constructor that takes formal parameters.

## Constraint Inheritance

Neither generic type parameters nor their constraints are inherited by a derived class, because generic type parameters are not members. (Remember, class inheritance is the property that the derived class has all the members of the base class.) It is a common practice to make new generic types that inherit from other generic types. In such a case, because the type parameters of the derived generic type become the type arguments of the generic base class, the type parameters must have constraints equal to (or stronger than) those on the base class. Confused? Consider Listing 12.27.

### LISTING 12.27: Inherited Constraints Specified Explicitly

```csharp
class EntityBase<T> where T : IComparable<T>
{
    // ...
}

// ERROR:
// The type 'U' must be convertible to
// 'System.IComparable<U>' to use it as parameter
// 'T' in the generic type or method
// class Entity<U> : EntityBase<U>
// {
//     ...
// }
```

In Listing 12.27, `EntityBase<T>` requires that the type argument `U` supplied for `T` by the base class specifier `EntityBase<U>` implement `IComparable<>`. Therefore, the `Entity<U>` class needs to require the same constraint on `U`. Failure to do so will result in a compile-time error. This pattern increases a programmer's awareness of the base class's type constraint in the derived class, avoiding the confusion that might otherwise occur when the programmer uses the derived class and discovers the constraint but does not understand where it comes from.

We have not covered generic methods yet; we'll get to them later in this chapter. For now, simply recognize that methods may also be generic and may also place constraints on the type arguments supplied for their type parameters. How, then, are constraints handled when a virtual generic method is inherited and overridden? In contrast to the situation with type parameters declared on a generic class, constraints on overriding virtual generic methods (or explicit interface) methods are inherited implicitly and may not be restated (see Listing 12.28).

### LISTING 12.28: Repeating Inherited Constraints on Virtual Members Is Prohibited

```csharp
class EntityBase
{
    public virtual void Method<T>(T t)
        where T : IComparable<T>
    {
        // ...
    }
}

class Order : EntityBase
{
    public override void Method<T>(T t)
    //    Constraints may not be repeated on overriding
    //    members
    //    where T : IComparable<T>
    {
        // ...
    }
}
```

In the generic class inheritance case, the type parameter on the derived class can be further constrained by adding not only the constraints on the base class (required), but also other constraints. However, overriding virtual generic methods need to conform exactly to the constraints defined by the base class method. Additional constraints could break polymorphism, so they are not allowed and the type parameter constraints on the overriding method are implied.

## ADVANCED TOPIC

## Constraint Limitations

Constraints are appropriately limited to avoid nonsensical code. For example, you cannot combine a class type constraint with a struct or class constraint. Also, you cannot specify constraints to restrict inheritance to special types such as `Object`, arrays, `System.ValueType`, `System.Enum` (enum), `System.Delegate`, or `System.MulticastDelegate`.

In some cases, constraint limitations are perhaps more desirable, but they still are not supported. The following subsections provide some additional examples of constraints that are not allowed.

## Operator Constraints Are Not Allowed

You cannot constrain a type parameter to a type that implements a particular method or operator, except via interface type constraints (for methods) or class type constraints (for methods and operators). Because of this, the generic `Add( )` in Listing 12.29 does not work.

### LISTING 12.29: Constraint Expressions Cannot Require Operators

```csharp
public abstract class MathEx<T>
{
    ...
    public static T Add(T first, T second)
    {
        // Error: Operator '+' cannot be applied to
        // operands of type 'T' and 'T'
        // return first + second;
    }
}
```

In this case, the method assumes that the `+` operator is available on all types that could be supplied as type arguments for `T`. But there is no constraint that prevents you from supplying a type argument that does not have an associated addition operator, so an error occurs. Unfortunately, there is no way to specify that an addition operator is required within a constraint, aside from using a class type constraint where the class type implements an addition operator.

More generally, there is no way to constrain a type to have a static method.

## OR Criteria Are Not Supported

If you supply multiple interfaces or class constraints for a type parameter, the compiler always assumes an AND relationship between constraints. For example, where `T : IComparable<>, IFormattable` requires that both `IComparable<>` and `IFormattable` are supported. There is no way to specify an OR relationship between constraints. Hence, an equivalent of Listing 12.30 is not supported.

### LISTING 12.30: Combining Constraints Using an OR Relationship Is Not Allowed

```csharp
public class BinaryTree<T>
    // Error: OR is not supported
    // where T: System.IComparable<T> || System.IFormattable
{
    ...
}
```

Supporting this functionality would prevent the compiler from resolving which method to call at compile time.

## Constraints of Type Delegate and Enum Are Not Valid

Delegate types, array types, and enumerated types may not be used as class type constraints, because they are all effectively “sealed” types. (If you are not familiar with delegate types, see Chapter 13.) Their base types—`System.Delegate`, `System.MultiCastDelegate`, `System.Array`,
