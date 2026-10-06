# ISO/IEC 14882:2017(E)

# 20.3.17

observer function
class member function (12.2.1) accesses the state of an object of the class but does not alter that state

> [Note 1 to entry: Observer functions are specified as const member functions (12.2.2.1). — end note]

# 20.3.18

referenceable type
type that is either an object type, a function type that does not have cv-qualifiers or a ref-qualifier, or a reference

> [Note 1 to entry: The term describes a type to which a reference can be created, including reference types. — end note]

# 20.3.19

replacement function
non-resolved function whose definition is provided by a C++ program

> [Note 1 to entry: Only one definition for such a function is in effect for the duration of the program's execution, as the result of clearning the program (5.2) and resolving the definitions of all translation units (6.5). — end note]

# 20.3.20

positional stream
stream (described in Clause 30) that can seek to a position that was previously encountered

# 20.3.21

required behavior
description of replacement function and handler function semantics apply to both the behavior by the implementation and the behavior of any such function in the program

> [Note 1 to entry: If such a function in a C++ program fails to meet the required behavior when it executes, the behavior is undefined. — end note]

# 20.3.22

reserved function
function, specified as part of the C++ standard library, that is defined by the implementation

> [Note 1 to entry: If a C++ program provides a definition for any reserved function, the results are undefined. — end note]

# 20.3.23

stable algorithm
alalgorithm preserves, as appropriate to the particular algorithm, the order of elements

> [Note 1 to entry: Requirements for stable algorithms are given in 20.5.5.7. — end note]

# 20.3.24

traits class
class that encapsulates a set of types and functions necessary for class templates and function templates to manipulate objects of types for which they are instantiated

# 20.3.25

valid but unspecified state
value of an object that is not specified except that the object's invariants are met and operations on the object behavior as specified for its type