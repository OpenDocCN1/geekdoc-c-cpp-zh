representation, even though the value of a member of the structure or union may be a trap representation.

7 When a value is stored in a member of an object of union type, the bytes of the object representation that do not correspond to that member may correspond to other members take unspecified values.

8 Where an operator is applied to a value that has more than one object representation, which object representation is used shall not affect the value of the result.52) Where a value is stored in an object using a type that has more than one object representation for that value, it is unspecified which representation is used, but a trap representation shall not be generated.

9 Loads and stores of objects with atomic types are done with memory_order_seq_cst semantics.

Forward references: declarations (6.7), expressions (6.5), Ivalues, arrays, and function descriptors (6.3.2.1), order and consistency (7.17.3).

# 6.2.6.2 Integer types

1 For unsigned integer types other than unsigned char, the bits of the object representation shall be divided into two groups: value bits and padding bits (there need not be of the latter). If there are N values, each bit shall represent a different power of 2 between 1 and 2^{N-1}, so objects of that type shall be capable of representing values from 0 to 2^{N-1} using a pure binary representation; this shall be known as the value representation. The values of padding bits are unspecified.53)

2 For signed integer types, the bits of the object representation shall be divided into three groups: value bits, padding bits, and the sign. There need not be any padding bits; signed char shall not have any padding bits. There shall be exactly one sign bit. Each bit that is a value bit shall have the same value as the same bit in the object representation of the corresponding unsigned type (if there are M bits in the signed type and N in the unsigned type, M ≤ N).

> 51) Thus, for example, structure assignment need not copy any padding bits.

> 52) It is possible for objects x and y with the same type T to have the same value when they are accessed as objects of T, but to have different values in other contexts. In particular, if defined for type T, x == y does not imply memcmp(x,y,sizeof(T))0. Furthermore, x != does not necessarily imply that x and y have the same value; other operations on types of T may distinguish between them.

> 53) Some combinations of padding bits might generate trap representations, for example, if one padding is a parity bit. Regardless, no arithmetic operation on valid values can generate a representation other than as part of an exceptional condition, which cannot occur with unsigned types. All other combinations of padding bits are alternative object representations of the value specified by the padding bits.