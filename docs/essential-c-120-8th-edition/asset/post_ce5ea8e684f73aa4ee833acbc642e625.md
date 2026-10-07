# Chapter 12: Generics

## Constraint Inheritance

Neither generic type parameters nor their constraints are inherited by a derived class, because generic type parameters are not members. (Remember, class inheritance is the property that the derived class has all the members of the base class.) It is a common practice to make new generic types that inherit from other generic types. In such a case, because the type parameters of the derived generic become the type arguments of the generic base class, the type parameters must have constraints equal to (or stronger than) those on the base class. Confused? Consider Listing 12.31.

Listing 12.31: Inherited Constraints Specified Explicitly

```sharp
public class EntityBase<T> where T : IComparable<T>
{
    // ...
}

ERROR:
// The type 'U' must be convertible to 'System.IComparable<U>
// to use it as parameter 'T' in the generic type or
// method
class Entity<U> : EntityBase<U>
{
    //...
}
```

In Listing 12.31, EntityBase<T> requires that the argument U supplied for T by the base class specifier EntityBase<U> implement IComparable<U>. Therefore, the Entity<U> class needs to require the same constraint on U. Failure to do so will result in a compile-time error. This pattern increases a programmer's awareness of the base class's type constraint, avoiding confusion that might otherwise occur if the programmer uses the derived class and discovers the constraint but does not understand where it comes from.

We have not covered generic methods yet; we'll get to them later in this chapter. For now, recognize that methods may be generic and may also place constraints on the type arguments supplied for their type parameters. How, then, are constraints handled when a virtual generic method is inherited and overridden? In contrast to the situation with type parameters declared on a generic class, constraints on overriding virtual generic methods (or explicit interface methods) are inherited implicitly and may not be restated (see Listing 12.32).

Listing 12.32: Repeating Inherited Constraints on Virtual Members Is Prohibited

```sharp
public class EntityBase {
    public virtual void Method<T>(T t)
    where T : IComparable<T>
    {
        // ...
    }
}
public class Order : EntityBase {
    public override void Method<T>(T t)
    // Constraints may not be repeated on overriding
    // members
    where T : IComparable<T>
    {
        // ...
    }
}
```

In the generic inheritance case, the type parameter on the derived class can be further constrained by adding not only the constraints on the base class (required), but also other constraints. However, overriding virtual generic methods need to conform exactly to the constraints defined by the base class method. Additional constraints could break polymorphism, so they are not allowed, and the type parameter constraints on the overriding method are implied.

## ADVANCED TOPIC

### Constraint Limitations

Constraints are appropriately limited to avoid nonsensical code. For example, you cannot combine a class type constraint with a struct or class constraint, or notnull with either type of constraint. Also, you cannot specify constraints that restrict inheritance to special types such as object, arrays, or System.ValueType.¹¹¹ You cannot have a constraint for a specific delegate type like Action, Func<T>, or related types.

In some cases, constraint limitations are perhaps more desirable, yet they are still not supported. Only having the ability to require a default constructor is perhaps one such limitation. The following subsections provide some additional examples of constraints that are not allowed.

### Operator Constraints Are Not Allowed

All generics implicitly allow for == and != comparisons, along with implicit casts to object, because everything is an object. You cannot constrain a type parameter to a type that implements a particular method or operator (other than in the aforementioned cases), except via interface type constraints (for methods) or class type constraints (for methods and operators). Because of this, the generic Add() does not work.

Listing 12.33: Constraint Expressions Cannot Require Operators

```sharp
public abstract class Math<T>
{
    public static T Add(T first, T second)
    {
        // Error: Operator '+' cannot be applied to
        // operands of type 'T' and 'T'
        // return first + second;
    }
}
```

In this case, the method assumes that the + operator is available on all types that could be supplied as type arguments for T. But there is no constraint that prevents you from supplying a type argument that does not have an associated addition operator, or an error occurs. Unfortunately, there is no way to specify that an addition operator is required within a constraint, from using a class type constraint where the class type implements an addition operator.

More generally, there is no way to constrain a type to a static method.

¹¹ System.Enum (enum), System.Delegate, and System.MulticastDelegate are supported starting in C# 7.3.

### OR Criteria Are Not Supported

If you supply multiple interfaces or class constraints for a type parameter, the compiler always assumes an AND relationship between constraints. For example, where T : IComparable<T>, IFormattable requires both IComparable<T> and IFormattable are supported. There is no way to specify an OR relationship between constraints. Hence, code equivalent to Listing 12.34 is not supported.

Listing 12.34: Combining Constraints Using an OR Relationship Is Not Supported

```sharp
public class BinaryTree<T>
    // Error: OR is not supported
    // where T: System.IComparable<T> // System.IFormattable
{
    //...
}
```

Supporting this functionality would prevent the compiler from resolving which method to call at compile time.

## Generic Methods

Earlier, you saw that it is a relatively simple matter to add a method to a type when the type is generic; such a method can use the type parameters declared by the type. You did this, for example, in the generic class examples we have seen so far.

Generic methods use generic type parameters, as generic types do. They can be declared in generic or nongeneric types. If declared in a generic type, their type parameters are distinct from those of their containing generic type. To declare a generic method, you specify the type parameters the same way you do for generic types: Add the type parameter declaration syntax immediately following the method name, as shown in the MathEx.Max<T> and MathEx.Min<T> examples in Listing 12.35.

In this example, the method is static, although this is not required.

Listing 12.35: Defining Generic Methods

```sharp
public static class MathEx {
    public static T Max<T>(T first, params T[] values)
    where T : IComparable<T> {
        T maximum = first;
        foreach(T item in values) {
            if(item.compareTo(maximum) > 0) {
                maximum = item;
            }
        }
        return maximum;
    }

    public static T Min<T>(T first, params T[] values)
    where T : IComparable<T> {
        T minimum = first;
        foreach(T item in values) {
            if(item.compareTo(minimum) < 0) {
                minimum = item;
            }
        }
        return minimum;
    }
}
```

Generic methods, like generic types, can include more than one type parameter. The arity (the number of type parameters) is an additional distinguishing characteristic of a method signature. That is, it is legal to have two methods with identical names and formal parameter types, as long as they differ in method type arity.

## Generic Method Inference

Just as type arguments are provided after the type name when using a generic type, so the method type arguments are provided after the method name. The code used to call the Min<T> and Max<T> methods looks like that shown in Listing 12.36 with Output 12.4.

Listing 12.36: Specifying the Type Parameter Explicitly

```sharp
Console.WriteLine(
  MathEx.Max<int>(7, 490));
Console.WriteLine(
  MathEx.Min<string>("R.O.U.S", "Fireswamp"));
```

# Output 12.4

```
490
ireswamp
```

Not surprisingly, the type arguments, int and string, correspond to the actual types used in the generic method calls. However, specifying the type arguments is redundant because the compiler can infer the type parameters from the formal parameters passed to the method. To avoid redundancy, you can exclude the type parameters from the call in all cases when the compiler is able to logically infer which type arguments you have intended. An example of this practice, which is known as **method type inference**, appears in Listing 12.37 with Output 12.5.

Listing 12.37: Inferring the Type Argument from the Arguments

```sharp
Console.WriteLine(
  MathEx.Max(7, 490)); // No type arguments!
Console.WriteLine(
  MathEx.Min("R.O.U.S", "Fireswamp"));
```

# Output 12.5

```
490
fireswamp
```
