
- Supportive of commonly accepted programming styles.
- Extensible to deal with user-defined types in ways similar to the way built-in types and standard-library types are handled.

For example, building the comparison criteria into a sort function is unacceptable because the same data can be sorted according to different criteria. This is why the C standard-library **qsort()** takes a comparison function as an argument rather than relying on something fixed, say, the < operator (§12.5). On the other hand, the overhead imposed by a function call for each comparison compromises **qsort()** as a building block for further library building. For almost every data type, it is easy to do a comparison without imposing the overhead of a function call.

Is that overhead serious? In most cases, probably not. However, the function call overhead can dominate the execution time for some algorithms and cause users to seek alternatives. The technique described in §25.2.3 of supplying comparison criteria through a template argument solves that problem for **sort()** and many other standard-library algorithms. The sort example illustrates the tension between efficiency and generality. It is also an example of how such tensions can be resolved. A standard library is not merely required to perform its tasks. It must also perform them so efficiently that users are not tempted to supply their own alternatives to what the standard offers.

Otherwise, implementers of more advanced features are forced to bypass the standard library in order to remain competitive. This would add a burden to the library developer and seriously complicate the lives of users wanting to stay platform-independent or to use several separately developed libraries.

The requirements of “primitiveness” and “convenience of common uses” can conflict. The former requirement precludes exclusively optimizing the standard library for common cases. However, components serving common, but nonprimitive, needs can be included in the standard library in addition to the primitive facilities, rather than as replacements. The cult of orthogonality must not prevent us from making life convenient for the novice and the casual user. Nor should it cause us to leave the default behavior of a component obscure or dangerous.

## 30.1.3 Description Style

A full description of even a simple standard-library operation, such as a constructor or an algorithm, can take pages. Consequently, I use an extremely abbreviated style of presentation. Sets of related operations are typically presented in tables:

## Some Operations

`p=op(b,e,x)` op does something to the range `[b:e)` and `x`, returning `p`; `foo(x)` foo does something to `x` but returns no result  
`bar(b,e,x)` Does `x` have something to do with `[b:e)`?

I try to be mnemonic when choosing identifiers, so **b** and **e** will be iterators specifying a range, **p** a pointer or an iterator, and **x** some value, all depending on context. In this notation, only the commentary distinguishes no result from a Boolean result, so you can confuse those if you try hard enough. For an operation returning a Boolean, the explanation usually ends with a question mark. Where an algorithm follows the usual pattern of returning the end of an input sequence to indicate “failure,” “not found,” etc. (§4.5.1, §33.1.1), I do not mention that explicitly.

Usually, such an abbreviated description is accompanied with a reference to the ISO C++ standard, some further explanation, and examples.

## 30.2 Headers

The facilities of the standard library are defined in the **std** namespace and presented as a set of headers. The headers identify the major parts of the library. Thus, listing them gives an overview of the library.

The rest of this subsection is a list of headers grouped by function, accompanied by brief explanations and annotated by references to where they are discussed. The grouping is chosen to match the organization of the standard.

A standard header with a name starting with the letter **c** is equivalent to a header in the C standard library. For every header `<X.h>` defining part of the C standard library in the global namespace and also in namespace **std**, there is a header `<cX>` defining the same names. Ideally, the names from a `<cX>` header do not pollute the global namespace (§15.2.4), but unfortunately (due to complexities of maintaining multilanguage, multi-operating-system environments) most do.

## Containers

- `<vector>` One-dimensional resizable array §31.4.2
- `<deque>` Double-ended queue §31.4.2
- `<forward_list>` Singly-linked list §31.4.2
- `<list>` Doubly-linked list §31.4.2
- `<map>` Associative array §31.4.3
- `<set>` Set §31.4.3
- `<unordered_map>` `<unordered_set>` Hashed associative array §31.4.3.2 Hashed set §31.4.3.2
- `<queue>` Queue §31.5.2
- `<stack>` Stack §31.5.1
- `<array>` One-dimensional fixed-size array §34.2.1
- `<bitset>` Array of bool §34.2.2

The associative containers **multimap** and **multiset** can be found in `<map>` and `<set>`, respectively. The **priority_queue** (§31.5.3) is declared in `<queue>`.

## General Utilities

`<utility>` Operators and pairs §35.5, §34.2.4.1  `<tuple>` Tuples §34.2.4.2  `<type_traits>`

- <typeindex>
- <functional>
- <memory>
- <scoped_allocator> <ratio>
- <chrono>
- <ctime>
- <iterator>

Type traits §35.4.1 Use a **type_info** as a key or a hash code §35.5.4 Function objects §33.4 Resource management pointers §34.3 Scoped allocators §34.4.4 Compile-time rational arithmetic §35.3 Time utilities §35.2 C-style date and time §43.6 Iterators and iterator support §33.1

Iterators provide the mechanism to make standard algorithms generic (§3.4.2, §33.1.4).

- <algorithm> <cstdlib>

## Algorithms

General algorithms §32.2
**bsearch()**, **qsort()** §43.7

A typical general algorithm can be applied to any sequence (§3.4.2, §32.2) of any type of element. The C standard library functions **bsearch()** and **qsort()** apply to built-in arrays with elements of types without user-defined copy constructors and destructors only (§12.5).

- <exception>
- <stdexcept>
- <cassert>
- <cerrno>
- <system_error>

## Diagnostics

Exception class §30.4.1.1 Standard exceptions §30.4.1.1 Assert macro §30.4.2 C-style error handling §13.1.1.2 System error support §30.4.3

Assertions using exceptions are described in §13.4.

- <string>
- <cctype> <cwctype> <cstring> <cwchar> <cstdlib> <cuchar> <regex>

## Strings and Characters

String of T Chapter 36 Character classification §36.2.1 Wide-character classification §36.2.1 C-style string functions §43.4 C-style wide-character string functions §36.2.1 C-style allocation functions §43.5 C-style multibyte characters
Regular expression matching Chapter 37

The **<cstring>** header declares the **strlen()**, **strcpy()**, etc., family of functions. The **<cstdlib>** declares **atof()** and **atoi()** which convert C-style strings to numeric values.

- <iosfwd>
- <iostream> <ios>
- <streambuf> <istream>
- <ostream> <iomanip> Manipulators §38.4.5.2

## Input/Output

Forward declarations of I/O facilities §38.1 Standard iostream objects and operations §38.1 iostream bases §38.4.4 Stream buffers §38.6 Input stream template §38.4.1 Output stream template §38.4.2

<sstream> <cctype> <fstream> <cstdio> <cwchar>

Streams to/from strings §38.2.2
Character classification functions §36.2.1
Streams to/from files §38.2.1
printf() family of I/O §43.3 printf()-style I/O of wide characters §43.3

Manipulators are objects used to manipulate the state of a stream (§38.4.5.2).

<locale> <clocale> <codecvt>

## Localization

Represent cultural differences Chapter 39 Represent cultural differences C-style Code conversion facets §39.4.6

A locale localizes differences such as the output format for dates, the symbol used to represent currency, and string collation criteria that vary among different natural languages and cultures.

<limits>
<climits>
<cfloat>
<cstdint>
<new>
<typeinfo>
<exception>
<initializer_list> <cstddef>
<cstdarg>
<csetjmp>
<cstdlib>
<ctime>
<csignal>

## Language Support

Numeric limits §40.2
C-style numeric scalar-limit macros §40.2
C-style numeric floating-point limit macros §40.2
Standard integer type names §43.7
Dynamic memory management §11.2.3 Run-time type identification support §22.5
Exception-handling support §30.4.1.1 initializer_list §30.3.1 C library language support §10.3.1 Variable-length function argument lists §12.2.4 C-style stack unwinding Program termination §15.4.3 System clock §43.6
