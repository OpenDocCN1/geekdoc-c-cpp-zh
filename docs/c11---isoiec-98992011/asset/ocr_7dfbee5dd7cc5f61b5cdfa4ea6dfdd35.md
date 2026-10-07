# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

2 When a value of integer type is converted to a real floating type, if the value being converted can be represented exactly in the new type, it is unchanged. If the value being converted is in the range of values that can be represented but cannot be represented exactly, the result is either the nearest higher or nearest lower representable value, chosen in an implementation-defined manner. If the value being converted is outside the range of values that can be represented, the behavior is undefined. Results of some implicit conversions may be represented in greater range and precision than that required by the new type (see 6.3.1.8 and 8.6.6.4).

# 6.3.1.5 Real floating types

+   1 When a value of real floating type is converted to a real floating type, if the value being converted can be represented exactly in the new type, it is unchanged. If the value being converted is in the range of values that can be represented but cannot be represented exactly, the result is either the nearest higher or nearest lower representable value, chosen in an implementation-defined manner. If the value being converted is outside the range of values that can be represented, the behavior is undefined. Results of some implicit conversions may be represented in greater range and precision than that required by the new type (see 6.3.1.8 and 8.6.6.4).

# 6.3.1.6 Complex types

+   1 When a value of complex type is converted to another complex type, both the real and imaginary parts follow the conversion rules for the corresponding real types.

# 6.3.1.7 Real and complex

+   1 When a value of real type is converted to a complex type, the real part of the complex result is determined by the conversion rules for the corresponding real type and the imaginary part of the complex result is a positive zero or an unsigned zero.

+   2 When a value of complex type is converted to a real type, the imaginary part of the complex value is discarded and the value of the real part is converted according to the conversion rules for the corresponding real type.

# 6.3.1.8 Usual arithmetic conversions

+   1 Many operations that operate on arithmetic type cause conversions and yield result in a similar way. The purpose is to determine a common real type for the operands and for the specified operands, each is converted, without change of type domain, to a type whose real type is the common real type. Unless explicitly stated, the common real type is also the real domain of the operands if they are the same, and complex otherwise. This pattern is called the *arithmetic conversions*:

First, if the real type of either operand is **long double**, the other operand is converted, without change of type domain, to a type whose

52

Language

§6.3.1.8