broadest possible type object.

The catch is that when you instantiate a generic collection type, you need to specify a specific type. That is, although a generic type or generic method, in general, can support a range of types, e.g., more than one types, for its "associated type(s)", one can only use the generic type/method by fixing its associated type(s) to a specific type(s) (allowed by the generic definitions).

The variables of an instantiated/specialized generic type are no longer "generic". They only work with that specific type.

The sample code uses a generic list `System.Collections.Generic.List<T>`, which is sort of a dynamic array, whose size can change at run time unlike the builtin array type.

The T in the angular brackets (<...>) is known as the "type parameter". It is just a placeholder (for the associated type), and it is customary to use the letter T (T for "Type"), if there is only one type parameter, although that is not required.

As stated, we define a generic type (and, a generic collection) "generically" (that is, over a range of different types), but we can only use it for a particular fixed associated type (i.e., its element type).

In the example, we use the `int` type:

```
var list = new List<int>();
```

This statement declares a variable `list` of type `List<int>`. An instance of the `List<int>` type can contain elements of type `int`, but nothing else. Note the relationship between the collection type `List<int>` and its associated element type `int`.