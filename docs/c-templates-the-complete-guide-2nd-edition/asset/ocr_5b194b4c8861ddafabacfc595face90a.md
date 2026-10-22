pointer; see is_scalar() on page 707) – a trivial class type (a class that has no virtual functions, no virtual base classes, no (indirectly) user-defined default constructor, copy/move constructor, copy/move assignment operator, or destructor, no initializer for nonstatic data members, no volatile members, and no nontrivial members) – an array of such types
– and cv-qualified versions of these types • Yields true if is_trivially_copyable_v<T> yields true and a trivial default constructor exists.

+   - Requires that the given type is either complete (see Section 10.3.1 on page 154) or (cv-qualified) void.

# std:: is_trivially_copyable < T >::value

+   - Yields true if the type is a “trivially copyable” type: – a scalar type (integral, float, enum, pointer; see is_scalar<> on page 707) – a trivial class type (a class that has no virtual functions, no virtual base classes, no (indirectly) user-defined default constructor, copy/move constructor, copy/move assignment operator, or destructor, no initializer for nonstatic data members, no volatile members, and no nontrivial members) – an array of such types – and cv-qualified versions of these types • Yields the same as is_trivial_v<T> except it can produce true for a class type without a trivial default constructor.

+   - In contrast to is_standard_layout<>, volatile members are not allowed, references are allowed, members might have different access, and members might be distributed among different (base) classes.

+   - Requires that the given type is either complete (see Section 10.3.1 on page 154) or (cv-qualified) void.

# std:: is_standard_layout < T >::value

+   - Yields true if the type has a standard layout, which, for example, makes it easier to exchange values of this type with other languages.
+   – a scalar type (integral, float, enum, pointer; see is_scalar<> on page 707)
+   – a standard-layout class type (no virtual functions, no virtual base classes, no nonstatic reference members, all nonstatic members are in the same (base) class defined with the same access, all members are also standard-layout types) – an array of such types
+   – and cv-qualified versions of these types • In contrast to is_trivial<>, volatile members are allowed, references are not allowed, members might not have different access, and members might not be distributed among different