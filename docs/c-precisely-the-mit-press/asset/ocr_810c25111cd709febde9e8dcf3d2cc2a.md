# Nullable Types over Value Types

A nullable type t? is used to represent missing values of type t, where t is a value type such as int, a non-null struct type, or a type parameter that has a struct constraint. A value of type t is either non-null and contains a proper value of type t, or is the unique null value. The default value of a nullable type is null. A nullable t? is an alias for System.Nullable<t> and is itself a value type.

A nullable type such as int? is useful for the custom using null to represent a missing value of reference type does not carry over to value types: null is not a legal value of the plain value type int. v1 and v2 of nullable type support the following:

+   - Read-only v1.HasValue of bool returns true if v is not null; false if it is null.
- Read-only v1.Value of type t returns the proper value in v1 if v1 is non-null and has t?; it throws InvalidOperationException if v is null.
- Standard comparisons: The implicit conversion from v of type t to t? gives a non-null value containing a copy of v. The implicit coercion from null to t? gives the null value.
- Standard explicit conversions: (t?) coerces from t to t? and is equivalent to t value.
- Lifted conversions: Whenever there is an implicit (or explicit) coercion from value type ts to t?, there is an implicit (or explicit) coercion from t? to t?.
- Boxing and unboxing conversions: Boxing of a non-null type t gives a boxed t (not a boxed t?); and boxing of a null t gives a null value. Unboxing of a non-null reference gives a non-null t value; and unboxing of a null reference gives a null t value.
- Lifted unary operators ++ -- ! : If argument and result type of an existing operator are non-null value types, then an additional lifted operator is automatically defined for the corresponding types. If the argument is null, the result is null; otherwise the underlying operator is applied to the proper value in the argument.
- Lifted binary operators + - % / ^ | << >> : If the argument and result type of an existing operator are non-null value types, then an additional lifted operator is automatically defined for the corresponding types. If any argument is null, the result is null; otherwise the underlying operator is applied to the proper value in the arguments. The corresponding compound assignment, as +=, is automatically defined for nullable types.
- Equality comparisons: v1==v2 is true if both v1 and v2 are null or both are non-null and contain the same value, false v1!=v2 is the negation of v1==v2. Unless v1.HasValue and v1.Value equals v1.HasValue.
- Ordering comparisons: v1<v2 and v1<=v2 and v1>v2 and v1>=v2 have type bool. A comparison evaluates to false if either is null; otherwise it compares the proper values in v1 and v2.

The nullable type bool? has values null, false, and true, as in the three-valued logic of the SQL language. The operators & and | have special definitions that compute a proper value when:

| xy | null | false | true | xy | null | false | true |
| --- | --- | --- | --- | --- | --- | --- | --- |
| null | null | false | null | null | null | null | true |
| false | false | false | false | false | false | true | true |
| true | null | false | true | true | true | true | true |