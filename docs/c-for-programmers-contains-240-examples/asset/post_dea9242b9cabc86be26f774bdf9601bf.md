
## 21.9 Technical Report 1

Technical Report 1 (TR1) describes proposed additions to the C++ Standard Library. Many of the libraries in TR1 will be accepted by the C++ Standards Committee but they are not considered part of the C++ standard until the next version is finalized. The library additions provide solutions for many common programming problems. We described the 11 Boost libraries in TR1 in Section 21.6; descriptions of the three additional TR1 libraries follow. Many libraries didn’t make it into TR1 due to time constraints. Technical Report 2 (TR2), which will be released shortly after C++0x, contains additional library proposals that weren’t included in TR1. The release of TR2 will bring even more functionality to the standard library without having to wait for another new standard.

### Unordered Associative Containers¹³

The Unordered Associative Containers library defines four new containers—unordered_set, unordered_map, unordered_multiset and unordered_multimap. These associative containers are implemented as hash tables. A hash table is split into sections sometimes called “buckets.” A key is used to determine where to store an element in the container. The key is passed to a hash function which returns a size_t. The size_t returned by the hash function determines the “bucket” that the value is placed in. If two values are equal, so are the size_ts returned by the hash function. Multiple values can be placed in the same “bucket.” You retrieve an element from the container using the key much as you do with a set or map. The key determines which “bucket” the value was placed in, then the “bucket” is searched for the value.

With unordered_set and unordered_multiset, the element itself is used as the key. unordered_map and unordered_multimap use a separate key to determine where to place the element—the arguments are passed as a pair< const Key, Value >. unordered_set and unordered_map require that all the keys used are unique; unordered_multiset and unordered_multimap don’t enforce that restriction. The containers are defined in the <unordered_set> and <unordered_map> headers.

### Mathematical Special Functions¹⁴

This library incorporates mathematical functions added to C99—the C standard published in 1999—that are missing in the C++ Standard. C99 supplies trigonometric, hyperbolic, exponential, logarithmic, power and special functions. This library adds those functions, among others, to C++ in the <cmath> header.

### Increased Compatibility with C99¹⁵

C++ evolved from the C programming language. Most C++ compilers can also compile C programs, but there are some incompatibilities between the languages. The goal of this library is to increase compatibility between C++ and C99. Most of this library involves adding items to C++ headers to support C99 features—this is often accomplished by including the corresponding C99 headers.

13. Matthew Austern, “A Proposal to Add Hash Tables to the Standard Library,” Document Number N1456=03-0039, April 9, 2003, www.open-std.org/jtc1/sc22/wg21/docs/papers/2003/n1456.html.

14. Walter E. Brown, “A Proposal to Add Mathematical Special Functions to the C++ Standard Library,” Document Number N1422=03-0004, February 24, 2003, std.dkuug.dk/jtc1/sc22/wg21/docs/papers/2003/n1422.html.

15. P. J. Plauger, “Proposed Additions to TR-1 to Improve Compatibility With C99,” Document Number N1568=04-0008, www.open-std.org/jtc1/sc22/wg21/docs/papers/2004/n1568.htm.

## 21.10 C++0x

The C++ Standards Committee is currently revising the C++ Standard. The last standard was published in 1998. Work on the new standard, currently referred to as C++0x, began in 2003. The new standard, likely to be released in 2009, includes the TR1 libraries and additions to the core language. Browse the C++0x section of the Deitel C++ Resource Center at www.deitel.com/cpplusplus/ and click C++0x in the Categories list to find current information on C++0x.

### Standardization Process

The International Organization for Standardization (ISO) oversees the creation of international programming language standards, including those for C and C++. Every addition or change to the current C++ standard must be approved by the ISO/IEC JTC 1/SC 22 Working Group 21 (WG21), the committee that maintains the C++ standard. This committee of volunteers from the C++ programming community meets twice a year to discuss issues pertaining to the standard. Smaller, unofficial meetings are held more frequently to consider proposals between official committee meetings. ISO requires at least 5 years between new drafts of a standard.

### Goals for C++0x¹⁶

Bjarne Stroustrup, creator of the C++ programming language, has expressed his vision for the future of C++—the main goals for the new standard are to make C++ easier to learn, improve library building capabilities, and increase compatibility with the C programming language.

## 21.11 Core Language Changes

A listing of proposed changes to the core language can be found at www.open-std.org/jtc1/sc22/wg21/docs/papers/2007/n2228.html. There are also links to the papers associated with each proposal. We briefly discuss only the core language changes that have been accepted into the working draft of the new standard. The number of proposals that make it into the working draft is likely to increase before the standard is finalized. The GCC C++ compiler has an optional C++0x mode which allows you to experiment with a number of the core language changes (gcc.gnu.org/gcc-4.3/cxx0x_status.html).

### Rvalue Reference¹⁷

The rvalue reference type in C++0x allows you to bind an rvalue (temporary object) to a non-const reference. An rvalue reference is declared as T&& (where T is the type of the object being referenced) to distinguish it from a normal reference T& (now called an lvalue reference). An rvalue reference can be used to effectively implement move semantics. This improves performance by preventing the compiler from making extra copies of large objects, an expensive operation. Rvalue references can also be used in “forwarding functions”—function objects that adapt a function to take fewer arguments (e.g., std::bind1st or function objects created using Boost.Bind). Normally, each reference parameter would need a const and non-const version to account for lvalues, const lvalues and rvalues. With rvalue references you need only one forwarding function.

### Clarification of Initialization of Class Objects by rvalues¹⁸

This proposal clarifies the writing in the standard regarding the use of rvalues as arguments to functions that receive their arguments by value. The new wording would allow compiler writers to implement move semantics rather than copy semantics if it can be determined that the rvalue is going to be removed from memory after the copy. This would increase performance by eliminating an extra copy constructor call.

### static_assert¹⁹

The static_assert declaration allows you to test certain aspects of the program at compile time. A static_assert declaration takes a constant integral expression and a string literal. If the expression evaluates to 0 (false), the compiler reports the error. The error message includes the string literal provided in the declaration. The static_assert declaration can be used at namespace, class or block scope.

The addition of static_assert makes learning C++ easier. The assertions can be used to provide more informative error messages when novice programmers make common mistakes such as using the wrong type of argument in a function call or template instantiation. They’re also useful in library development—incorrect usage of the library can be reported much more effectively.

### extern template²⁰

The keyword extern indicates that a variable or function is defined either later in the current file or in a separate file. This proposal allows the extern keyword to provide the same functionality for templates, which would help prevent extra instantiations of the template. This can improve compilation times and reduce the size of a program’s object code.

### Extended friend Declarations²¹

This proposal clarifies wording in the C++ standard with respect to friend declarations and templates.
