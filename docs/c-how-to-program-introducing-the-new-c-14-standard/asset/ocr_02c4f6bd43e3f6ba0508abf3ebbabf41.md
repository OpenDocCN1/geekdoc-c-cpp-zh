a `double` parameter—the function will still work correctly, provided this is not a narrowing conversion (discussed in [Section 4.11.7](#)).

# 6.5.3 Argument-Promotion Rules
and Implicit Conversions¹

1. Promotions and conversions are complex topics discussed in Section 4 and the beginning of Section 5 of the C++ standard.

Sometimes, argument values that do not correspond precisely to the parameter types in the function prototype can be converted by the compiler to the proper type before the function is called. These conversions occur as specified by C++’s **promotion rules**, which indicate the *implicit conversions allowed* between fundamental types. An `int` can be converted to a `double`. A `double` can also be converted to an `int`, but this narrowing conversion *truncates* the `double`’s fractional part—recall from [Section 4.11.7](#) that list initializers do not allow narrowing conversions. Keep in mind that `double` variables can hold numbers of much greater magnitude than `int` variables, so the loss of data in a narrowing conversion may be considerable. Values may also be modified when converting large integer types to small integer types (e.g., `long` to `short`), signed to unsigned or unsigned to signed. Unsigned integers range from 0 to approximately twice the positive range of the corresponding signed type.