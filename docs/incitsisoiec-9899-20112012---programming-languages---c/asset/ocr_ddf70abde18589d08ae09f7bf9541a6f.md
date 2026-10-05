There are three complex types, designated as float _Complex, double _Complex, long double _Complex^{43)} (Complex types are a conditional feature that implementations do not support; see 6.10.8.3.) The real floating and complex types are collectively called the floating types.

For each floating type there is a corresponding real type, which is always a real floating type. For complex types, it is the same type. it is type given by deleting the keyword _Complex from the type name.

Each complex type has the same representation and alignment requirements as any other type containing exactly two elements of the corresponding real type; the first element is equal to the real type, and the second element to the imaginary part, of the complex number.

The type char, the signed and unsigned integer types, and the floating types are collectively called the basic types. The basic types are object types. Even if the implementation defines two or more types to have the same representation, they are nevertheless different types^{44)}

The three types char, signed char, and unsigned char are collectively called the character types. The implementation char to have the same range, representation, and behavior as either signed char or unsigned char^{45)}

An enumeration comprises a set of named integer constant values. Each distinct enumeration constitutes a different enumerated type.

The type char, the signed and unsigned integer types, and the enumerated types are collectively called integer types. The integer and real floating types are collectively called real types.

Integer and floating types are collectively called arithmetic types. Each arithmetic type belongs to one type domain: the real type domain comprises the real types, the complex type domain comprises the complex types.

The void type comprises an empty set of values; it is an incomplete object type that cannot be completed.

> 43) A specification for imaginary types is in annex G.

> 44) An implementation may define new keywords that provide alternative ways to designate a basic (or any other type); this does not violate the requirement that all basic types are different. Implementation-defined keywords shall have the form of an identifier reserved for use as described in 7.1.3.

> 45) CHAR_MIN, defined in <limits.h>, will have one of the values 0 or SCHAR_MIN, and this can be used to distinguish the two options. Irrespective of the choice made, char is a separate type from the other and is not compatible with it.