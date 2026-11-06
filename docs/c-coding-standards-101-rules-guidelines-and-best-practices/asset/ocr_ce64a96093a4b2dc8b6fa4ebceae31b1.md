Corollary. In header files, don't write namespace-level **using** directives or **using** declarations; instead, explicitly namespace-qualify all names. (The second rule follows from the first, because headers can never know what other header **#include**s might appear after them.)

60. Avoid allocating and deallocating memory in different modules.

*Put things back where you found them:* Allocating memory in one module and deallocating it in a different module makes your program fragile by creating a subtle long-distance dependency between those modules. They must be compiled with the same compiler version and same flags (notably debug vs. *NDEBUG*) and the same standard library implementation, and in practice the module allocating the memory had better still be loaded when the deallocation happens.

61. Don't define entities with linkage in a header file.

*Repetition causes bloat:* Entities with linkage, including namespace-level variables or functions, have memory allocated for them. Defining such entities in header files results in either link-time errors or memory waste. Put all entities with linkage in implementation files.

62. Don't allow exceptions to propagate across module boundaries.

*Don't throw stones into your neighbor's garden:* There is no ubiquitous binary standard for C++ exception handling. Don't allow exceptions to propagate between two pieces of code unless you control the compiler and compiler options used to build both sides; otherwise, the modules might not support compatible implementations for exception propagation. Typically, this boils down to: Don't let exceptions propagate across module/subsystem boundaries.

63. Use sufficiently portable types in a module's interface.

*Take extra care when living on the edge (of a module):* Don't allow a type to appear in a module's external interface unless you can ensure that all clients understand the type correctly. Use the highest level of abstraction that clients can understand.

# Templates and Genericity

64. Blend static and dynamic polymorphism judiciously.

*So much more than a mere sum of parts:* Static and dynamic polymorphism are complementary. Understand their tradeoffs, use each for what it's best at, and mix them to get the best of both worlds.

65. Customize intentionally and explicitly.

*Intentional is better than accidental, and explicit is better than implicit:* When writing a template, provide points of customization knowingly and correctly, and document them clearly. When using a template, know how the template intends for you to customize it for use with your type, and customize it appropriately.

66. Don't specialize function templates.

*Specialization is good only when it can be done correctly:* When extending someone else's function template (including `std::swap`), avoid trying to write a specialization; instead, write an overload of the function template, and put it in the namespace of the type(s) the overload is designed to be used for. (See Item 57.) When you write your own function template, avoid encouraging direct specialization of the function template itself.