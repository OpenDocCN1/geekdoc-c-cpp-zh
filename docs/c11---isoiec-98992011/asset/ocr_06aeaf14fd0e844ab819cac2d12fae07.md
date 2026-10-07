# 6.5.2.4 Postfix increment and decrement operators

Constraints

The operand of the postfix increment or decrement operator shall have atomic, qualified, or unqualified real or pointer type, and be a modifiable value.

Semantics

The result of the postfix ++ operator is the value of the operand. As a side effect, the value of the operand is incremented (that is, the value 1 of the appropriate type is added to it). See the discussions of additive operators and compound assignment for information on constraints, types, and conversions and the effects of operations on pointers. The value computation of the result is sequenced before the side effect of updating the stored value of the operand. With respect to indeterminately-sequenced function, the operation of postfix ++ is a single evaluation. Postfix ++ on atomic type is a read-modify-write operation with memory_order_seq_cst memory semantics.98

The postfix -- operator is analogous to the postfix ++ operator, except that the value of the operand is subtracted (that is, the value 1 of the appropriate type is subtracted from it).

**Forward references:** additive operators (6.5.6), compound assignment (6.5.16.2).

# 6.5.2.5 Compound literals

Constraints

The type must specify a complete object type or an array of unknown size, but not a variable length array type.

All the constraints for initializer lists in 6.7.9 also apply to compound literals.

Semantics

A postfix expression of a parenthesized type followed by a brace-enclosed list of initializers is a compound literal. It provides an unnamed object

> 98 Where a pointer to an atomic object can be formed and E has integer type, E++ is equivalent to the following code sequence where T is the type of E:

```
*addr = &E;
T old = *addr;
T new;
do {
    new = old + 1;
} while (!atomic_compare_exchange_strong(addr, &old, new));
```

Special case may be used if it has literal type: 6.5.16.2.