from an underlying type to its nullable form in an implicit manner. Furthermore, all the implicit numeric conversions apply to nullable forms, too:

```
int i = 42;
int? ni = i;   // int  -> int?
long? nl1 = i; // int  -> long?
long? nl2 = ni; // int? -> long?
```

When converting between values of different nullable types, a null-value represented by a HasValue property retuning false will simply result in a null value of the target type. If the value isn't null, the underlying value will be converted and wrapped in a value of the target type.

On the explicit conversion side, nullables support the lifted form of the underlying type's explicit conversions. In addition, you can also go from a nullable value to its non-nullable type. In such a case, an exception will be thrown if the original value is the null value:

```
long? l = 123;
int? i = (int?)l;
int? n = null;
int j = (int)n; // Will throw an InvalidOperationException
```

# Reference Conversions

For reference types, a wide range of conversions exist, most of which require a further discussion about object-oriented programming principles, which are covered in Chapter 14. For completeness, we simply mention the supported conversions here and illustrate them with a couple of examples.

Implicit conversions exist between an object of a certain reference type and any of its base types or interfaces it implements. As a result, every object of a reference type can be converted to an object of type System.Object:

```
List<int> xs = new List<int> { 1, 2, 3 };
IList<int> list = xs; // Every List<T> implements IList<T>.
IEnumerable<int> sequence = list; // Every IList<T> is an IEnumerable<T>.
```

Arrays support covariant conversion, which is discussed as part of our coverage of generics in Chapter 15, “Generic Types and Methods,” which simply means you can assign an