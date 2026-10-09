to do that.

Typically, you instantiate a structure type by calling an appropriate constructor with the `new` operator. Every structure type has at least one constructor. That's an implicit parameterless constructor, which produces the default value of the type. You can also use a default value expression to produce the default value of a type.

If all instance fields of a structure type are accessible, you can also instantiate it without the `new` operator. In that case you must initialize all instance fields before the first use of the instance.

In the case of the built-in value types, use the corresponding literals to specify a value of the type.

# Passing structure-type variables by reference

When you pass a structure-type variable to a method as an argument or return a structure-type value from a method, the whole instance of a structure type is copied. That can affect the performance of your code in high-performance scenarios that involve large structure types. You can avoid value copying by passing a structure-type variable by reference. Use the `ref`, `out`, or `in` method parameter modifiers to indicate that an argument must be passed by reference.

Use `ref return` to return a method result by reference.

```
`ref struct`
```

You can use the `ref` modifier in the declaration of a structure type. Instances of a `ref struct` type are allocated on the stack and can't escape to the managed heap.

Typically, you define a `ref struct` type when you need a type that also includes data members of `ref struct` types.

To declare a `ref struct` as `readonly`, combine the `readonly` and `ref` modifiers in the type declaration (the `readonly` modifier must come before the `ref` modifier).

544