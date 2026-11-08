standard-layout types)

+   - an array of such types
+   - and its cv-qualified versions of those types
+   - In contrast to `is_trivial`, volatile members are allowed, references are not allowed, members might not have different access, and members might not be distributed among different base classes.
+   - Requires that the given type (for arrays, the base type) is either complete (see Section 10.3.1 on page 154) or (cv-qualified) `void`.

```
`std::is_pod<T>::value`
```

+   - Yields true if `T` is a POD type (POD).
+   - Objects of such types can be copied by copying the underlying storage (e.g. using `memcpy()`).
+   - Same as: `is_trivial<T> && is_standard_layout<T>`.
+   - Yields false for:
+     - classes that don't have a trivial default constructor, copy/move constructor, copy/move assignment, or destructor
+     - classes that have virtual members or virtual base classes
+     - classes that have volatile or reference members
+     - classes that have members in different (base) classes or with different access
+     - the types of lambda expressions (called closure types)
+     - functions
+     - `void`
+     - types removed from these types
+   - Requires that the given type is either complete (see Section 10.3.1 on page 154) or (cv-qualified) `void`.

```
`std::is_literal_type<T>::value`
```

+   - Yields true if the given type is a valid pure literal type for a `constexpr` function (which notably excludes any type requiring nontrivial destruction).
+   - Yields true if `T` is a literal type:
+     - a scalar type (integral, float, enum, pointer; see `is_scalar()` on page 707)
+     - a reference
+     - a class type with at least one `constexpr` constructor that is not a copy/move constructor (in each (base) class, no user-defined or virtual destructor or any (base) class or member, and where every initialization for nonstatic data members is a constant expression)
+     - an array of such types
+   - Requires that the given type is either complete (see Section 10.3.1 on page 154) or (cv-qualified) `void`.

```
`std::is_empty<T>::value`
```

+   - Yields true if `T` is a class type but not a union type, whose objects hold no data.
+   - Yields true if defined as class or struct with:
+     - no nonstatic data members other than bit-fields of length 0
+     - no virtual member functions
+     - no virtual base classes
+     - no nonempty base classes
+   - Requires that given type is complete (see Section 10.3.1 on page 154) if it is a class/struct (an incomplete union is undefined).

```
`std::is_polymorphic<T>::value`
```

+   - Yields true if `T` is a polymorphic class type (a class that declares or inherits a virtual function).
+   - Requires that the given type is either complete (see Section 10.3.1 on page 154) or (cv-qualified) `void`.

```
`std::is_abstract<T>::value`
```

+   - Yields true if `T` is an abstract class type (a class for which no objects can be created because it has at least one pure virtual member function).
+   - Requires that the given type is either complete (see Section 10.3.1 on page 154).

```
`std::is_final<T>::value`
```

+   - Yields true if `T` is a final class type (a class or union that can't serve as a base class in another class).
+   - For all non-class/union types such as `int`, it returns false (this, this is ...).