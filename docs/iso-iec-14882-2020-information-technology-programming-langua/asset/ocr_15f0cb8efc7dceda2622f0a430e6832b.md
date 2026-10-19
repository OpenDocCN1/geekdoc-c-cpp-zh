# 3.21
**handler function**
[defns.handler]

⟨library⟩ non-reserved function whose definition may be provided by a C++ program

> [Note 1 to entry: A C++ program may designate a handler function at various points in its execution by supplying a pointer to the function when calling any of the library functions that install handler functions (Clause 17). — end note]

# 3.22
**ill-formed program**
[defns.ill.formed]

program that is not well-formed (3.60)

# 3.23
**implementation-defined behavior**
[defns.impl.defined]

behavior, for a well-formed program construct and correct data, that depends on the implementation and that each implementation documents

# 3.24
**implementation-defined strict total order over pointers**
[defns.order.ptr]

⟨library⟩ implementation-defined strict total ordering over all pointer values such that the ordering is consistent with the partial order imposed by the builtin operators <, >, <=, >=, and <=

# 3.25
**implementation limits**
[defns.impl.limits]

restrictions imposed upon programs by the implementation

# 3.26
**iostream class templates**
[defns.iostream.templates]

⟨library⟩ templates that are declared in header <iosfwd> and take two template arguments

> [Note 1 to entry: The arguments are named charT and traits. The argument charT is a character container class, and the argument traits is a class which defines additional characteristics and functions of the character type represented by charT necessary to implement the iostream class templates. — end note]

# 3.27
**locale-specific behavior**
[defns.locale.specific]

behavior that depends on local conventions of nationality, culture, and language that each implementation documents

# 3.28
**modifier function**
[defns.modifier]

⟨library⟩ class member function other than a constructor, assignment operator, or destructor that alters the state of an object of the class

# 3.29
**move assignment**
[defns.move.assign]

⟨library⟩ assignment of an rvalue of some object type to a modifiable lvalue of the same type

# 3.30
**move construction**
[defns.move.constr]

⟨library⟩ direct-initialization of an object of some type with an rvalue of the same type

# 3.31
**multibyte character**
[defns.multibyte]

sequence of one or more bytes representing a member of the extended character set of either the source or the execution environment

> [Note 1 to entry: The extended character set is a superset of the basic character set (5.3). — end note]

# 3.32
**NTCTS**
[defns.ntcts]

⟨library⟩ sequence of values that have character type that precede the terminating null character type value charT()