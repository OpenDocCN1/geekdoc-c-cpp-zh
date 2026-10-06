# 12.12 Struct Value Expression

To create and initialize a value of struct type (section 14), use the struct value creation expression:

```
new $(actual-list)
```

It creates a new value of struct type $ and then calls that constructor in struct $ whose signature matches the argument types in actual-list, a possibly empty comma-separated list of expressions.

The actual-list is evaluated from left to right to obtain a list of argument values. If this is empty, the default constructor is called; otherwise a matching constructor is found, and the argument values are bound to the constructor's parameters. A value of type $ is created in the computer's store, a base class constructor is implicitly called, and the finally constructor is executed to initialize the struct value. The value of the constructor call is the newly created struct value, whose type is $.

# 12.13 Instance Test Expression

The instance test e is t whether of e can be converted to t by a reference conversion, a boxing conversion, or an unboxing conversion. It is evaluated by first evaluating to a value v. If v is not null and is a reference to an object of class C, where C can be converted to t, the result is true; otherwise, if e evaluates to a value that can be boxed or unboxed to obtain a value of t, the result is true; otherwise false. if e has reference type and the result is false. The instance test considers only reference conversions, boxing conversions, and unboxing conversions (section 5.3), but not user-defined conversions (section 10.18) or conversions between simple types (section 5.3.1).

The type t may be a struct type or another value type. This is useful if expression v has reference type, possibly being a reference to a boxed value (section 14.1); if v had value type too, the expression would be either constant true or constant false.

# 12.14 Instance Test and Cast Expression

The expression x as t is equivalent to a combined test and cast: (x is t ? (t)x : (t)null) but evaluates x only once. It has type. The type t must be a reference type.