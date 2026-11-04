The fact that null was supported only for reference types was unfortunate, exposing to the surface something that should really have been an implementation detail. Whether a type supports null as a possible value should be decoupled from the type's physical representation.

For example, think of databases where an integer-valued column can contain null values. If you don't know the shoe size of a customer (and your database schema permits this situation), leave it empty. Whether shoe sizes are represented as values or references into some table is totally irrelevant in this discussion. Either way, they should have the right to be null.

One way to circumvent this problem in the .NET 1.0 time frame was to store a Boolean-valued “nullness” indicator next to the value-typed data:

```
class Person
{
    private int _shoeSize;
    private bool _hasKnownShoeSize;
}
```

This is definitely a cumbersome pattern in a world where null is already a well-established concept. To rectify this situation, .NET 2.0 introduced the concept of nullable value types.

# UNION TYPES

Types are like sets that define all the permitted "values" instances can have. In fact, the analogy between type theory and set theory is well defined in academia. This is nothing you should really need to know to write code in C#, but some other languages make this correspondence very visible.

F# is such an example, where nullability is expressed in the form of option types. An option type is constructed over an underlying type, extending its value domain with an additional None value. For example, consider the int type, which does not have None as a valid value:

```
let a : int = 1
let b : int = None        (* invalid *)
```

In other words, the type is not nullable. To give the type nullability support, an option type is created:

```
let c : int option = Some(1)
let d : int option = None    (* valid *)
```

The option type is a sample of a discriminated union: The set of values it supports consists of the union of other sets. With the option type, this is the union of the underlying type's domain (here, int) and the singleton None value.