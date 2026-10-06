# ISO/IEC 14882:2017(E)

```
static constexpr int min_exponent10;
```

Minimum negative integer such that 10 raised to is in the range of normalized floating-point numbers.^{196}

Meaningful for all floating-point types.

```
static constexpr int max_exponent;
```

Maximum positive integer such that radix raised to power less than that is a representable finite floating-point number.^{199}

Meaningful for all floating-point types.

```
static constexpr int max_exponent10;
```

Maximum positive integer such that 10 raised to is in the range of representable finite floating-point numbers.^{200}

Meaningful for all floating-point types.

```
static constexpr bool has_infinity;
```

true if the type has a representation for positive infinity.

Meaningful for all floating-point types.

Shall be true for all specializations in which is_iec559 == false.

```
static constexpr bool has_quiet_NaN;
```

true if the type has a representation for a quiet (non-signaling) "Not a Number"^{201}

Meaningful for all floating-point types.

Shall be true for all specializations in which is_iec559 == false.

```
static constexpr bool has_signaling_NaN;
```

true if the type has a representation for a signaling "Not a Number"^{202}

Meaningful for all floating-point types.

Shall be true for all specializations in which is_iec559 == false.

```
static constexpr float_denom_style has_denom;
```

denom_present if the type allows subnormal values (variable number of exponent bits)^{203}, denom_absent if the type does not allow subnormal values, and denom_indeterminate if it is indeterminate at compile time whether the type allows subnormal values.

Meaningful for all floating-point types.

```
static constexpr bool has_denom_loss;
```

true if loss occurs as a denormalization, rather than as an inexact result.^{204}