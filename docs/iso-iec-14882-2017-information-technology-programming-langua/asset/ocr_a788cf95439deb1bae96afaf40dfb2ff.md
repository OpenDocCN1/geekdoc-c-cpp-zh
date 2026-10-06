# ISO/IEC 14882:2017(E)

Rationale: Dynamic exceptions were a deprecated feature that was complex and brittle in use. They interacted badly with the type system, which became a more significant issue in this International Standard where (non-dynamic) exception specifications are of the function type.

Effect on original feature: A Valid C++ 2014 declaration, member function declaration, function pointer declaration, or function reference declaration, if it has a potentially throwing exception specification, will be rejected as ill-formed in this International Standard. Violating a non-throwing exception specification will be considered terminate rather than unexpected and might not perform stack unwinding prior to such a call.

# C.4.8 Clause 20: library introduction [diff.cpp14.library]

20.5.1.2

Change: New headers.
Rationale: New functionality.

Effect on original feature: The following C++ 2014 headers are new: <any>, <execution>, <filesystem>, <memory_resource>, <optional>, <string_view>, and <variant>. Valid C++ 2014 code includes headers with names that may be invalid in this International Standard.

20.5.4.2

Change: New namespaces.
Rationale: Namespace revisions for features of standard library that might be incompatible with existing programs.

Effect on original feature: The global namespaces followed by an arbitrary sequence of digits are reserved for future standardization. Valid C++ 2014 code that uses a top-level name, e.g., std2, may be invalid in this International Standard.

# C.4.9 Clause 23: general utilities library [diff.cpp14.utilities]

23.1.4.3

Change: Constructors removing allocators.
Rationale: No implementation consensus.

Effect on original feature: Valid C++ 2014 code may fail to compile or change meaning in this International Standard. Specifically, constructing a std::function with an allocator is ill-formed and uses-allocator construction will not pass an allocator to std::function constructors in this International Standard.

23.11.2.2

Change: Different constraint on conversions from unique_ptr.
Rationale: Adding array support to shared_ptr, the syntax shared_ptr<T[]> and shared_ptr<T[N]>.

Effect on original feature: Valid C++ 2014 code may fail to compile or change meaning in this International Standard. For:

# C.4.10 Clause 24: string resources [diff.cpp14.string]

24.3.2

Change: Non-const .data() member added.
Rationale: The lack of a non-const .data() differed from the similar member of std::vector. This change regularizes behavior for this International Standard.

Effect on original feature: Overloaded functions which have differing code paths for char* and const char* arguments will execute correctly when called with a non-const string's .data() member in this International Standard.