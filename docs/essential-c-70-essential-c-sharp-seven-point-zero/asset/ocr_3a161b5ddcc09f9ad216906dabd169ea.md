# **LISTING 12.27:** Inherited Constraints Specified Explicitly

```
```C#  
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
```

In Listing 12.27, `EntityBase<T>` requires that the type argument `U` supplied for `T` by the base class specifier `EntityBase<U>` implement `IComparable<>`. Therefore, the `Entity<U>` class needs to require the same constraint on `U`. Failure to do so will result in a compile-time error. This pattern increases a programmer's awareness of the base class's type constraint in the derived class, avoiding the confusion that might otherwise occur when the programmer uses the derived class and discovers the constraint but does not understand where it comes from.

We have not covered generic methods yet; we'll get to them later in this chapter. For now, simply recognize that methods may also be generic and may also place constraints on the type arguments supplied for their type parameters. How, then, are constraints handled when a virtual generic method is inherited and overridden? In contrast to the situation with type parameters declared on a generic class, constraints on overriding virtual generic methods (or explicit interface) methods are inherited implicitly and may not be restated (see Listing 12.28).

# **LISTING 12.28:** Repeating Inherited Constraints on Virtual Members Is Prohibited

```
```C#  
    class EntityBase  
    {  
        public virtual void Method<T>(T t)  
            where T : IComparable<T>  
        {  
            // ...  
        }  
    }  
```
```