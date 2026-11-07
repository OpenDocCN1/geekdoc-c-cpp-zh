associative containers are implemented as hash tables. A **hash table** is split into sections sometimes called “**buckets.**” A key is used to determine where to store an element in the container. The key is passed to a **hash function** which returns a size_t. The size_t returned by the hash function determines the “bucket” that the value is placed in. If two values are equal, so are the size_ts returned by the hash function. Multiple values can be placed in the same “bucket.” You retrieve an element from the container using the key much as you do with a set or map. The key determines which “bucket” the value was placed in, then the “bucket” is searched for the value.

With **unordered_set** and **unordered_multiset**, the element itself is used as the key. **unordered_map** and **unordered_multimap** use a separate key to determine where to place the element—the arguments are passed as a pair<const Key, Value>. **unordered_set** and **unordered_map** require that all the keys used are unique; **unordered_multiset** and **unordered_multimap** don’t enforce that restriction. The containers are defined in the <unordered_set> and <unordered_map> headers.

# *Mathematical Special Functions*<sup>12</sup>

This library incorporates mathematical functions added to **C99**—the C standard published in 1999—that are missing in the C++ Standard. C99 supplies trigonometric, hyperbolic, exponential, logarithmic, power and special functions. This library adds those functions, among others, to C++ in the <cmath> header.

# *Increased Compatibility with C99*<sup>13</sup>

C++ evolved from the C programming language. Most C++ compilers can also compile C programs, but there are some incompatibilities between the languages. The goal of this library is to increase compatibility between C++ and C99. Most of this library involves adding items to C++ headers to support C99 features—this is often accomplished by including the corresponding C99 headers.

# 23.8 C++0x

The C++ Standards Committee is currently revising the C++ Standard. The last standard was published in 1998. Work on the new standard, currently referred to as C++0x, began in 2003. The new standard, likely to be released in late 2011 or early 2012, includes the TR1 libraries and additions to the core language. Browse the C++0x section of the Deitel C++ Resource Center at www.deitel.com/cplusplus/ and click C++0x in the Categories list to find current information on C++0x.

# *Standardization Process*

The **International Organization for Standardization (ISO)** oversees the creation of international programming language standards, including those for C and C++. Every addition or change to the current C++ standard must be approved by the ISO/IEC JTC 1/SC 22 Working Group 21 (WG21), the committee that maintains the C++ standard. This com-

12. Walter E. Brown, “A Proposal to Add Mathematical Special Functions to the C++ Standard Library,” Document Number N1422=03-0004, February 24, 2003, std.dkuug.dk/jtc1/sc22/wg21/docs/papers/2003/n1422.html.

13. P. J. Plauger, “Proposed Additions to TR-1 to Improve Compatibility With C99,” Document Number N1568=04-0008, www.open-std.org/jtc1/sc22/wg21/docs/papers/2004/n1568.htm.