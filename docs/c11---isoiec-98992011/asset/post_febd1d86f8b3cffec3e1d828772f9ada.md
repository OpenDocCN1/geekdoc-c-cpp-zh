
# ISO/IEC 9899:2011 (E)
# © ISO/IEC 2011 – All rights reserved

qualified "float" and is a pointer to a qualified type.

+ 30 EXAMPLE 2 The type designated as "struct tag *[5] (float)" has type "array of pointer to function returning struct tag. The array length has five and the function has a single parameter of type float. Its type category is array.

Forward references: compatible and composite type (6.2.7), declarations (6.7).

## 6.2.6 Representations of types

### 6.2.6.1 General

The representations of all types are unspecified except stated in this subclause.

Except for bit-fields, objects are composed of contiguous sequences of one or more bytes, the number, order, and encoding of which are either explicitly specified or implementation-defined.

Values stored in unsigned bit-fields and objects of type char shall be represented using pure binary notation.

Values stored in non-bit-field objects of any other type of $n \times CHAR\_BIT$ bits, where $n$ is the size of an object in bytes, the value may be copied into an object of type unsigned by memcpy; the resulting set of bytes is called the object representation of value.

Values stored in bit-fields of $m$ bits, where $m$ is the size that the bit-field comprises in addressable unit it holds. Two values (other than NaNs) with the same object representation compare, but values that have different object representations.

Certain objects represent a value of the object type. If the stored value of an object has such a representation and is read by an expression that does not have character, the behavior is undefined. If such a representation is produced by a side effect that modifies any part of the object by an expression that does not have character, the behavior is undefined. Such representation is called a trap representation.

When a value is stored in an object of structure or union, including a member, the bytes of the object representation correspond to any padding bytes takes unspecified values.

A positional representation for integers uses binary digits 0 and 1, in which values represented by successive bits are additive and are multiplied by successive powers of 2, except the bit with the highest position (Adapted American National Dictionary for Information Processing Systems.). A byte contains $CHAR\_BIT$ bits, and the values of type unsigned char range from 0 to $2^{CHAR\_BIT} - 1$. Thus, any variable may be initialized to a trap representation without undefined behavior until a proper value is stored in an object, even though the value of member of structure or union may be a trap representation.

+ 7 When a value is stored in a member of object of union type, the bytes of the object representation do not correspond to that member but correspond to other members take unspecified values.

+ 8 Where an operator is applied to a value that has more than one object representation, which representation is used shall not affect the value of the result. Where a value is stored in an object using a type that has more than one object representation, it is unspecified but a trap representation shall not be generated.

+ 9 Loads and stores of objects with atomic types are done with memory_order_seq_cst semantics.

Forward references: declarations (6.7), expressions (6.5), lvalues, arrays, and function identifiers (6.3.2.1), order and consistency (7.17.3).

## 6.6.2 Integer types

- For unsigned type other than unsigned char, the bits of the object representation shall be divided into two groups: value bits and padding bits (need not any the latter). If there are $N$ values, each bit shall represent a different power of 2 between 1 and $2^{N-1}$, so that objects of type shall be capable of representing values from 0 to $2^{N-1}$ using a pure binary representation; this shall be known as the value representation. The values of any padding bits are unspecified.

- For signed integer types, the bits of the object representation shall be divided into three groups: value bits, padding bits, and sign bit. There need not any padding bits; signed char shall not have any padding bits. There shall be exactly one sign bit. Each bit that is a value bit shall have the same value as the bit in the representation of the unsigned type (if there are $M$ values in the signed type and $N \le M$). If the sign bit is zero, it shall not affect the resulting value. If the sign bit is 1, the value shall be modified in one of the following ways:
    - the corresponding value with sign bit 0 is negated (sign and magnitude);
    - the sign bit has the value $-(2^M)$ (two’s complement);
    - the sign bit has the value $-(2^M - 1)$ (ones’ complement).

Which of these applies is implementation-defined, as whether the value with sign bit 1 and all value bits zero (the first two), or with sign bit and all value bits 1 (ones' complement), is a trap representation or a normal value. In the case of sign and magnitude and ones' complement, if this representation is a normal value it is called a negative zero.

- If the implementation negative zeros, they shall be generated only by:
    - the &, ^, ~, <<, and >> operators with operands that produce such a value;
    - the +, -, /, and % operators where one operand is a negative zero and the result is zero;
    - compound assignment operators based on the above cases.

It is unspecified whether these cases actually generate a negative zero or a normal value, and whether a negative zero becomes a normal zero stored in an object. If the implementation does not support negative zeros, the behavior of the &, ^, ~, <<, and >> operators that would produce such a value is undefined.

The values of any padding bits are unspecified. A valid (non-trap) object representation of a signed integer type where the sign bit is zero is a valid object representation of the corresponding unsigned type, and shall represent the same value. For any integer, the object representation where all the bits are zero shall be a representation of the value zero in that type.

The precision of an integer is the number of bits to represent values, excluding any sign and padding bits. The width of an integer type is the same but including any sign bit; thus for unsigned integer types the two values are the same, while for signed types the width is greater than the precision.
