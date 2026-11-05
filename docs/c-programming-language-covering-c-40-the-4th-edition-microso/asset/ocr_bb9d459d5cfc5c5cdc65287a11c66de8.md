Unlike a variable of a reference type, a variable of a value type can contain the value `null` only if the value type is a nullable type. For every non-nullable value type, there is a corresponding nullable value type denoting the same set of values plus the value `null`.

Assignment to a variable of a value type creates a *copy* of the value being assigned. This differs from assignment to a variable of a reference type, which copies the reference but not the object identified by the reference.

# ### 4.1.1 The System.ValueType Type

All value types implicitly inherit from the class `System.ValueType`, which in turn inherits from class `object`. It is not possible for any type to derive from a value type, and value types are thus implicitly sealed (§10.1.2).

Note that `System.ValueType` is not itself a *value-type*. Rather, it is a *class-type* from which all *value-types* are automatically derived.

> > **ERIC LIPPERT**  This point is frequently confusing to novices. I am often asked, “But how is it possible that a value type derives from a reference type?” I think the confusion arises as a result of a misunderstanding of what “derives from” means. Derivation does not imply that the layout of the bits in memory of the base type is somewhere found in the layout of bits in the derived type. Rather, it simply implies that some mechanism exists whereby members of the base type may be accessed from the derived type.

# ### 4.1.2 Default Constructors

All value types implicitly declare a public parameterless instance constructor called the *default constructor*. The default constructor returns a zero-initialized instance known as the *default value* for the value type:

+   - For all *simple-types*, the default value is the value produced by a bit pattern of all zeros:
+     - For `byte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, and `ulong`, the default value is `0`.
+     - For `char`, the default value is `'\x0000'`.
+     - For `float`, the default value is `0.0f`.
+     - For `double`, the default value is `0.0d`.
+     - For `decimal`, the default value is `0.0m`.
+     - For `bool`, the default value is `false`.