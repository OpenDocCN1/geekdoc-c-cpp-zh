Structure types have *value semantics*. That is, a variable of a structure type contains an instance of the type. By default, variable values are copied on assignment, passing an argument to a method, and returning a method result. In the case of a structure-type variable, an instance of the type is copied.

Typically, you use structure types to design small data-centric types that provide little or no behavior. For example, .NET uses structure types to represent a number (both integer and real), a Boolean value, a Unicode character, a System.DateTime. If you're focused on the behavior of a type, consider defining a class. Class types have *reference semantics*. That is, a variable of a class type contains a reference to an instance of the type, not the instance itself.

Because structure types have *value semantics*, we recommend you to define *immutable* structure types.

# readonly struct

You use the `readonly` modifier to declare that a structure type is immutable:

All data members of a `readonly` struct must be read-only as follows:

+   - Any field declaration must have the `readonly` modifier

+   - Any property, including auto-implemented ones, must be read-only. A property may have an `init` accessor. That guarantees that no member of a `readonly` struct modifies the state of the struct. That means that other instance members except constructors are implicitly `readonly`.

> In a `readonly` struct, a data member of a mutable reference type still can mutate its own state. For example, you can't replace a System.Collections.Generic.List<T> instance, but you can add new elements to it.

# readonly instance members

You can also use the `readonly` modifier to declare that an instance member doesn't