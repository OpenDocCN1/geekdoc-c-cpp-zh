The analogy of a boxing class should not be used as more than a helpful tool for picturing how boxing works conceptually. There are numerous subtle differences between the behavior described by this specification and the behavior that would result from boxing being implemented in precisely this manner. end note]

# 11.2.9 Implicit dynamic conversions

An implicit dynamic conversion exists from an expression of type dynamic to any type T. The conversion is dynamically bound (§12.3.3), which means that an implicit conversion will be sought at run-time from the run-time type of the expression to T. If no conversion is found, a run-time exception is thrown.

This implicit conversion seemingly violates the advice in the beginning of §11.2 that an implicit conversion should never cause an exception. However, it is not the conversion itself, but the finding of the conversion that causes the exception. The risk of run-time exceptions is inherent in the use of dynamic binding. If dynamic binding of the conversion is not desired, the expression can be first converted to object, and then to the desired type.

[Example: The following illustrates implicit dynamic conversions:

```
object o = "object";
dynamic d = "dynamic";
string s1 = o; // Fails at compile-time - no conversion exists
string s2 = d; // Compiles and succeeds at run-time
int i = d; // Compiles but fails at run-time - no conversion exists
```

The assignments to s2 and i both employ implicit dynamic conversions, where the binding of the operations is suspended until run-time. At run-time, implicit conversions are sought from the run-time type of d – string – to the target type. A conversion is found to string but not to int. end example]

# 11.2.10 Implicit constant expression conversions

An implicit constant expression conversion permits the following conversions:

+   - A constant-expression (§12.20) of type int can be converted to type sbyte, byte, short, ushort, uint, or ulong, provided the value of the constant-expression is within the range of the destination type.
+   - A constant-expression of type long can be converted to type ulong, provided the value of the constant-expression is not negative.

# 11.2.11 Implicit conversions involving type parameters

For a type-parameter T that is known to be a reference type (§15.2.5), the following implicit reference conversions (11.2.7) exist:

+   - From T to its effective base class C, from T to any base class of C, and from T to any interface implemented by C.
+   - From T to an interface-type I in T’s effective interface set and from T to any base interface of I.
+   - From T to a type parameter U provided that T depends on U (§15.2.5). [Note: Since T is known to be a reference type, within the scope of T, the run-time type of U will always be a reference type, even if U is not known to be a reference type at compile-time. end note]
+   - From the null literal (§7.4.5.7) to T.

For a type-parameter T that is not known to be a reference type (§15.2.5), the following conversions involving T are considered to be boxing conversions (11.2.8) at compile-time. At run-time, if T is a value type, the conversion is executed as a boxing conversion. At run-time, if T is a reference type, the conversion is executed as an implicit reference conversion or identity conversion.

+   - From T to its effective base class C, from T to any base class of C, and from T to any interface implemented by C. [Note: C will be one of the types System.Object, System.ValueType, or System.Enum (otherwise T would be known to be a reference type). end note]