qualified "float" is a pointer to be qualified.

EXAMPLE 2 The type designated as struct tag (*[5]) float) has "array of pointer to function returning struct tag". The array has length five and the function has a single parameter of type float. Its category is array.

Forward references: compatible type and composite type (6.2.7), declarations (6.7).

# 6.2.6 Representations of types

# 6.2.6.1 General

The representations of all types are unspecified except as stated in this subclause.

Except for bit-fields, objects are composed of contiguous sequences of one or more bytes, the number, order, and encoding of which are either explicitly specified or implementation-defined.

Values stored in unsigned bit-fields and objects of type unsigned char shall be represented using a pure binary notation.${49)}

Values stored in non-bit-field objects of any other object type consist of n × CHAR_BIT bits, where n is the size of an object of that, in bytes. The value may be copied into an object of type unsigned char [n] (e.g., by memcpy); the resulting set of bytes is called the object representation of the value. Values stored in bit-fields consist of m bits, where m is the size specified for the bit-field. The object representation is the set of m bits-fields in the addressable storage unit holding it. Two values (other than NaNs) with the same object representation compare equal, but values that compare may have different object representations.

Certain object representations need not represent a value of the object type. If the stored value of an object has such a representation and is read by an lvalue expression does not have character type, the behavior is undefined. If such a representation is produced by a side effect that modifies any or part of the object by an lvalue expression does not have character type, the behavior is undefined.${50)} Such a representation is called a trap representation.

When a value is stored in an object of structure or union type, including in a member object, the bytes of the object representation that correspond to any padding take unspecified values.${51)} The value of a structure or union object is never a trap

> 49) A positional representation for integers that uses the binary digits 0 and 1, in which the values represented by successive bits are additive, with 1, and are multiplied by successive powers of 2, except perhaps the bit with the highest position. (Adapted from the American Dictionary for Information Processing Systems.). Byte contains CHAR_BIT bits, and the values of type unsigned char range from 0 to 2CHAR_BIT – 1.

> 50) Thus, an automatic variable can be initialized to a trap representation without causing undefined behavior, but the value cannot be used until a proper value is stored in it.