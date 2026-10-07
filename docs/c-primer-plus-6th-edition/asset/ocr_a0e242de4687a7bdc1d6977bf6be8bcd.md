# Chapter 18 Visiting with the New C++ Standard

One change is relaxing the constraints on what qualifies as “Plain Old Data,” or POD. In C++98, POD is a scalar type (a one-value type, such as int or double) or an old-fashioned structure with no constructors, base classes, private data, virtual functions, and so on. The idea that a POD was something for it's safe to make a byte-by-byte copy. Still is the idea, but C++11 recognizes one can remove some C++98 restrictions and still have a viable POD. This helps low-level programming because some low-level operations, such as using the C functions for byte-wise copying or binary I/O, require PODs.

Another change is making unions more flexible by allowing them to have constructors and destructors, but with some restrictions on other properties, for example, not allowing virtual functions. Unions are often utilized when minimizing the amount of memory used, and the new rules allow programmers to bring more flexibility and capability to these situations.

C++11 addresses memory alignment issues. Computer systems can restrict how data is stored in memory. For example, one system might require that a double value be stored at an even-numbered memory location, whereas another might require the storage to begin at a location that is a multiple of eight. The alignof operator (see Appendix E,“Other Operators”) provides information on the alignment requirements for a type or object. The alignas keyword specifies control over the alignment used. The constexpr mechanism expands the ability of the compiler to evaluate during compile expressions that evaluate to a constant value. The low-level aspect of this allows const variables to be stored in read-only memory, which is particularly useful in embedded programming. (Variables, const or otherwise, that are initialized during runtime, are stored in random-access memory).

# Miscellaneous

C++11 follows the lead of C99 in allowing for implementation-dependent extended integer types. These types, for example, could be used on a system with 128-bit integers. Extended types are supported in the C header file stdint.h and in the C++11 version, cstdint.

C++11 provides a mechanism, the literal operator, for creating user-defined literals. Using this mechanism, instance, one can define binary literals, such as 101001b, which the corresponding literal operator will convert to an integer value.

C++11 has a debugging tool called assert. It is a macro that checks during runtime if an assertion is false and displays a message and calls abort() if the assertion is false. The assertion would typically be about something the programmer thinks be true at that point in the program. C++11 adds the static_assert, which can be used to test assertions during compile time. The primary motivation is to make it easier to debug templates for, which instantiation takes place during compile time, not runtime.

C++11 provides more support for metaprogramming, which is creating programs that create or modify other programs or even themselves. In C++ this can be done during compile time using templates.