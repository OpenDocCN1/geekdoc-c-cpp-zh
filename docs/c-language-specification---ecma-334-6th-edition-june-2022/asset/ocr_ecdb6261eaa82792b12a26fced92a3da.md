+   - From char to ushort, int, uint, long, ulong, float, double, or decimal.

+   - From float to double.

Conversions from int, uint, long or ulong to float and from long or ulong to double may cause a loss of precision, but will never cause a loss of magnitude. The other implicit numeric conversions never lose any information.

There are no predefined implicit conversions to the char type, so values of the other integral types do not automatically convert to the char type.

# ### 10.2.4 Implicit enumeration conversions

An implicit enumeration conversion permits a *constant_expression* (§11.20) with any integer type and the value zero to be converted to any *enum_type* and to any *nullable_value_type* whose underlying type is an *enum_type*. In the latter case the conversion is evaluated by converting to the underlying *enum_type* and wrapping the result (§8.3.11).

# ### 10.2.5 Implicit interpolated string conversions

An implicit interpolated string conversion permits an *interpolated_string_expression* (§11.7.3) to be converted to `System.IFormattable` or `System.FormattableString` (which implements `System.IFormattable`). When this conversion is applied, a string value is not composed from the interpolated string. Instead an instance of `System.FormattableString` is created, as further described in §11.7.3.

# ### 10.2.6 Implicit nullable conversions

The implicit nullable conversions are those nullable conversions (§10.6.1) derived from implicit predefined conversions.

# ### 10.2.7 Null literal conversions

An implicit conversion exists from the null literal to any reference type or nullable value type. This conversion produces a null reference if the target type is a reference type, or the null value (§8.3.11) of the given nullable value type.

# ### 10.2.8 Implicit reference conversions

The implicit reference conversions are:

+   - From any *reference_type* to object and dynamic.

+   - From any *class_type* S to any *class_type* T, provided S is derived from T.

+   - From any *class_type* S to any *interface_type* T, provided S implements T.

+   - From any *interface_type* S to any *interface_type* T, provided S is derived from T.

+   - From an *array_type* S with an element type S_I to an *array_type* T with an element type T_I, provided all of the following are true:

+     - S and T differ only in element type. In other words, S and T have the same number of dimensions.

+     - An implicit reference conversion exists from S_I to T_I.