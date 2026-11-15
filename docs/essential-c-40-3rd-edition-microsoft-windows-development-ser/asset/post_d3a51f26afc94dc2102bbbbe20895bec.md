
multiple base class constraints are not allowed since it is not possible to derive from multiple classes. Similarly, base class constraints cannot be specified for sealed classes or specific structs. For example, C# does not allow a constraint for a type parameter to be derived from string or System.Nullable<T>.

## struct/class Constraints

Another valuable generic constraint is the ability to restrict type parameters to a value type or a reference type. The compiler does not allow specifying System.ValueType as the base class in a constraint. Instead, C# provides special syntax that works for reference types as well. Instead of specifying a class from which T must derive, you simply use the keyword struct or class, as shown in Listing 11.24.

### Listing 11.24: Specifying the Type Parameter As A Value Type

```
public struct Nullable<T> :
    IFormattable, IComparable,
    IComparable<Nullable<T>>, INullable
    where T : struct
{
    // ...
}
```

Because a base class constraint requires a particular base class, using struct or class with a base class constraint would be pointless, and in fact could allow for conflicting constraints. Therefore, you cannot use struct and class constraints with a base class constraint.

There is one special characteristic for the struct constraint. It limits possible type parameters as being only value types while at the same time preventing type parameters that are System.Nullable<T> type parameters. Why? Without this last restriction, it would be possible to define the nonsense type Nullable<Nullable<T>>, which is nonsense because Nullable<T> on its own allows a value type variable that supports nulls, so a nullable-nullable type becomes meaningless. Since the nullable operator (?) is a C# shortcut for declaring a nullable value type, the Nullable<T> restriction provided by the struct constraint also prevents code such as the following:

```
int? number // Equivalent to Nullable<Nullable<int> if allowed
```

## Multiple Constraints

For any given type parameter, you may specify any number of interfaces as constraints, but no more than one class, just as a class may implement any number of interfaces but inherit from only one other class. Each new constraint is declared in a comma-delimited list following the generic type and a colon. If there is more than one type parameter, each must be preceded by the where keyword. In Listing 11.25, the EntityDictionary class contains two type parameters: TKey and TValue. The TKey type parameter has two interface constraints, and the TValue type parameter has one base class constraint.

### LISTING 11.25: Specifying Multiple Constraints

```
public class EntityDictionary<TKey, TValue>
    : Dictionary<TKey, TValue>
    where TKey : IComparable<TKey>, IFormattable
    where TValue : EntityBase
{
    ...
}
```

In this case, there are multiple constraints on TKey itself and an additional constraint on TValue. When specifying multiple constraints on one type parameter, an AND relationship is assumed. TKey must implement IComparable<TKey> and IFormattable, for example.

Notice there is no comma between each where clause.

## Constructor Constraints

In some cases, it is desirable to create an instance of a type parameter inside the generic class. In Listing 11.26, the New() method for the EntityDictionary<TKey, TValue> class must create an instance of the type parameter TValue.

### LISTING 11.26: Requiring a Default Constructor Constraint

```
public class EntityBase<TKey>
{
    private TKey _Key;

    public TKey Key
    {
        get{ return _key; }
        set{ _key = value; }
    }
}

public class EntityDictionary<TKey, TValue> :
    Dictionary<TKey, TValue>
    where TKey : IComparable<TKey>, IFormattable
    where TValue : EntityBase<TKey>, new()
{
    // ...

    public TValue New(TKey key)
    {
        TValue newEntity = new TValue();
        newEntity.Key = key;
        Add(newEntity.Key, newEntity);
        return newEntity;
    }

    // ...
}
```

Because not all objects are guaranteed to have public default constructors, the compiler does not allow you to call the default constructor on the type parameter. To override this compiler restriction, you add the text `new()` after all other constraints are specified. This text is a **constructor constraint**, and it forces the type parameter decorated with the constructor constraint to have a default constructor. Only the default constructor constraint is available. You cannot specify a constraint for a constructor with parameters.

## Constraint Inheritance

Constraints are inherited by a derived class, but they must be specified explicitly on the derived class. Consider Listing 11.27.

### LISTING 11.27: Inherited Constraints Specified Explicitly

```
class EntityBase<T> where T : IComparable<T>
{
    // ...
}
```

```
// ERROR:
// The type 'T' must be convertible to 'System.IComparable<T>'
// In order to use it as parameter 'T' in the generic type or
// method.
```

```
// class Entity<T> : EntityBase<T>
// {
//     ...
// }
```

Because EntityBase requires that T implement IComparable<T>, the Entity class needs to explicitly include the same constraint. Failure to do so will result in a compile error. This increases a programmer's awareness of the constraint in the derived class, avoiding confusion when using the derived class and discovering the constraint but not understanding where it comes from.

In contrast, constraints on generic override (or explicit interface) methods are inherited implicitly and may not be restated (see Listing 11.28).

### LISTING 11.28: Inherited Constraints Specified Explicitly

```
class EntityBase<T> where T : IComparable<T>
{
    public virtual void Method<T>(T t)
        where T : IComparable<T>
    {
        // ...
    }
}
```

```
class Entity<T> : EntityBase<T>
{
    public virtual void Method<T>(T t)
        // Error: Constraints may not be
        // repeated on overriding members
        where T : IComparable<T>
    {
        // ...
    }
}
```

In the inheritance case the type parameter on the base class can be additionally constrained by adding not only the constraints on the base class (required), but also additional constraints as well. However, overriding members need to conform to the “interface” defined in the base class method. Additional constraints could break polymorphism, so they are not allowed and the type parameter constraints on the override method are implied.

## Constraint Limitations

Constraints are appropriately limited to avoid nonsense code. For example, you cannot combine a base class constraint with a struct or class constraint, nor can you use Nullable<T> on struct constraint type parameters. Also, you cannot specify constraints to restrict inheritance to special types such as object, arrays, System.ValueType, System.Enum (enum), System.Delegate, and System.MulticastDelegate.

In some cases, constraint limitations are perhaps more desirable, but they still are not supported. The following subsections provide some additional examples of constraints that are not allowed.

## Operator Constraints Are Not Allowed

Another restriction on constraints is that you cannot specify a constraint that a class supports on a particular method or operator, unless that method or operator is on an interface. Because of this, the generic Add() in Listing 11.29 does not work.

### LISTING 11.29: Constraint Expressions Cannot Require Operators

```
public abstract class MathEx<T>
{
    public static T Add(T first, T second)
    {
        // Error: Operator '+' cannot be applied to
        // operands of type 'T' and 'T'.
        return first + second;
    }
}
```

In this case, the method assumes that the + operator is available on all types. However, because all types support only the methods of object (which does not include the + operator), an error occurs. Unfortunately, there is no way to specify the + operator within a constraint; therefore, creating an add method in this way is a lot more cumbersome. One reason for this limitation is that there is no way to constrain a type to have a static method. You cannot, for example, specify static methods on an interface.
