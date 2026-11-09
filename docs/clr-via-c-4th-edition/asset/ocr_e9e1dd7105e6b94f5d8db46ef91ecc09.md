+   3. For each instance field defined by the type, compare the value in the `this` object with the value in the `obj` object by calling the field's `Equals` method. If any fields are not equal, return `false`.
+   4. Return `true`. `Object`'s `Equals` method is not called by `ValueType`'s `Equals` method.

Internally, `ValueType`'s `Equals` method uses reflection (covered in Chapter 23, "Assembly Loading and Reflection") to accomplish step 3. Because the CLR's reflection mechanism is slow, when defining your own value type, you should override `Equals` and provide your own implementation to improve the performance of value equality comparisons that use instances of your type. Of course, in your own implementation, do not call `base.Equals`.

When defining your own type, if you decide to override `Equals`, you must ensure that it adheres to the four properties of equality:

+   - **`Equals` must be reflexive**; that is, `x.Equals(x)` must return `true`.
+   - **`Equals` must be symmetric**; that is, `x.Equals(y)` must return the same value as `y.Equals(x)`.
+   - **`Equals` must be transitive**; that is, if `x.Equals(y)` returns `true` and `y.Equals(z)` returns `true`, then `x.Equals(z)` must also return `true`.
+   - **`Equals` must be consistent**. Provided that there are no changes in the two values being compared, `Equals` should consistently return `true` or `false`.

If your implementation of `Equals` fails to adhere to all of these rules, your application will behave in strange and unpredictable ways.

When overriding the `Equals` method, there are a couple more things that you'll probably want to do:

+   - **Have the type implement the `System.IEquatable<T>` interface's `Equals` method** This generic interface allows you to define a type-safe `Equals` method. Usually, you'll implement the `Equals` method that takes an `Object` parameter to internally call the type-safe `Equals` method.
+   - **Overload the `==` and `!=` operator methods** Usually, you'll implement these operator methods to internally call the type-safe `Equals` method.

Furthermore, if you think that instances of your type will be compared for the purposes of sorting, you'll want your type to also implement `System.IComparable`'s `CompareTo` method and `System.IComparable<T>`'s type-safe `CompareTo` method. If you implement these methods, you'll also want to overload the various comparison operator methods (`<`, `<=`, `>`, `>=`) and implement these methods internally to call the type-safe `CompareTo` method.