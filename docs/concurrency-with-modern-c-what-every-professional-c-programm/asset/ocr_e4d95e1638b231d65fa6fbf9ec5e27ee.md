Where expression

| Where expression | Description |
| --- | --- |
| const_where_expression | Selects elements with non-mutating operations. |
| where_expression | Selects elements with mutating operations. |
| where | Generated const_where_expression and where expression. |

# 7.5.2.3 Casts

Cast operations cast element-wise or split or concat between SIMD objects and single ones.

Casts

| Where expression | Description |
| --- | --- |
| simd_cast and static_simd_cast | Performs a element-wise static cast. |
| to_fixed_size, to_compatible, and to_native | Performs an element-wise ABI cast. |
| split | Splits a single SIMD object to multiple objects. |
| concat | Concatenates multiple SIMD objects into a single SIMD object. |

# 7.5.2.4 Algorithms

The SIMD algorithms are applied to two SIMD objects and return a SIMD object.

Algorithms

| Algorithms | Description |
| --- | --- |
| min | Applies the min operation element-wise and returns a SIMD object. |
| max | Applies the min operation element-wise and returns a SIMD object. |
| minmax | Applies the minmax operation element-wise and returns a SIMD object. |
| clamp | Applies the clamp operation element-wise and returns a SIMD object. |

The clamp algorithm applies element-wise the following operation for i in [0, size() ):