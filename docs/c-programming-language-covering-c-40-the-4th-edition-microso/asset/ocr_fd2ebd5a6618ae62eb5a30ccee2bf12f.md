For an explicit reference conversion to succeed at runtime, the value of the source operand must be null, or the actual type of the object referenced by the source operand must be a type that can be converted to the destination type by an implicit reference conversion (§6.1.6) or boxing conversion (§6.1.7). If an explicit reference conversion fails, a System.InvalidCastException is thrown.

Reference conversions, implicit or explicit, never change the referential identity of the object being converted. In other words, while a reference conversion may change the type of the reference, it never changes the type or value of the object being referred to.

# ### 6.2.5 Unboxing Conversions

An unboxing conversion permits a reference type to be explicitly converted to a value-type. An unboxing conversion exists from the types object, dynamic, and System.ValueType to any non-nullable-value-type, and from any interface-type to any non-nullable-value-type that implements the interface-type. Furthermore, type System.Enum can be unboxed to any enum-type.

An unboxing conversion exists from a reference type to a nullable-type if an unboxing conversion exists from the reference type to the underlying non-nullable-value-type of the nullable-type.

A value type S has an unboxing conversion from an interface type I if it has an unboxing conversion from an interface type Iₐ and Iₐ has an identity conversion to I.

A value type S has an unboxing conversion from an interface type I if it has an unboxing conversion from an interface or delegate type Iₐ and either Iₐ is variance-convertible to I or I is variance-convertible to Iₐ (§13.1.3.2).

An unboxing operation consists of first checking that the object instance is a boxed value of the given value-type, and then copying the value out of the instance. Unboxing a null reference to a nullable-type produces the null value of the nullable-type. A struct can be unboxed from the type System.ValueType, since that is a base class for all structs (§11.3.2).

Unboxing conversions are described further in §4.3.2.

# ### 6.2.6 Explicit Dynamic Conversions

An explicit dynamic conversion exists from an expression of type dynamic to any type T. The conversion is dynamically bound (§7.2.2), which means that an explicit conversion will be sought at runtime from the runtime type of the expression to T. If no conversion is found, a runtime exception is thrown.

If dynamic binding of the conversion is not desired, the expression can be first converted to object, and then to the desired type.