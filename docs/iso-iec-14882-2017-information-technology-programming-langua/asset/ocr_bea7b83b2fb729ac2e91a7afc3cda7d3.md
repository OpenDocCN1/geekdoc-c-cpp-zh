# ISO/IEC 14882:2017(E)

gram. If these components do not meet their requirements, this document places no requirements on the implementation.

+   2 In particular, the effects are defined in the following cases:

+   (2.1) for replacement functions (21.6.2), if the installed replacement function does not implement the semantics of the applicable behavior: paragraph.

+   (2.2) for handler functions (21.6.3.3, 21.8.4.1), if the installed handler function does not implement the semantics of the applicable behavior: paragraph when instantiating a template component, if the operations on

+   (2.3) for types used as template arguments if the type do not implement the semantics of the applicable Requirements (20.5.3.5, 26.2, 27.2, 28.3, 29.3). On such types can report a failure by throwing an exception unless otherwise specified.

+   (2.4) if any replacement function or handler destructor exits via an exception, unless specifically allowed in the applicable behavior: paragraph.

+   (2.5) if an incomplete type (6.9) is used as a template argument when instantiating a template unless specifically allowed for that component.

# 20.5.4.9 Function arguments [res.on.arguments]

+   1 Each of the following applies to all functions in the C++ standard library, unless explicitly stated otherwise.

+   (1.1) If an argument to a function has an invalid value (such as a value outside the domain of the function or a pointer invalid for it), the behavior is undefined.

+   (1.2) If an argument is described as being a reference, the pointer actually passes to the function which has a value such that all accesses and communications to objects (that would be valid if the pointer pointed to the first element of such an array) are in fact valid.

+   (1.3) If an argument binds to a value reference, the implementation may assume that this parameter is a unique reference to the form T& and [Note: If the parameter is a generic of T and type of u is bound, the argument binds to an value reference (17.8.2.1) and this is not covered by the previous sentence. — end note][ If a program casts a value to std::move(x), the program is effectively asking that the function to treat value as the argument as a temporary. The implementation is free to optimize all checks which might be needed if the argument — end note]

# 20.5.4.10 Library object access [res.on.objects]

+   1 The behavior of an object is undefined if called across library functions from different threads may introduce a data race. The conditions under which this may occur are in 20.5.5.9. [Note: Modifying an object of a library type that is shared between threads risks undefined behavior unless objects of that type are explicitly specified as shareable without data races or the users use a locking mechanism. — end note]

+   2 If an object library type is accessed, and the getting of the object's lifetime (6.8) does not happen before the access, or the access does not happen before the end of the object's lifetime, the behavior is undefined unless specified. — end note

# 20.5.4.11 Requires paragraph [res.on.required]

Violation of the preconditions specified in a function's Requires: paragraph results in undefined behavior unless the function's Throws: paragraph throwing an exception when the precondition is violated.

§ 20.5.4.11 ©ISO/IEC 2017 — All reserved 471