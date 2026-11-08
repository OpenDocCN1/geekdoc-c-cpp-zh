
also include the headers used by the definition of our template—in this case `x...` and `<p>` only. You may find this amounts to tens of thousands of lines of code because headers like `<create-on-container>` contain many template definitions of their own.

This is a real problem in practice because it considerably increases the time needed by the compiler to compile significant programs. We will therefore examine some possible ways to approach this problem, including precompiled headers (see Section 9.3 on page 746) and the use of explicit template instantiation (see Section 14.5 on page 626).

Despite this built-in issue, we do recommend following this inclusion model to organize your templates when possible until a better mechanism becomes available. At the time of writing this book in 2017, such a mechanism is in the works: modules, which is introduced in Section 17.1 on page 936. The language mechanism that allows the programmer to use compiler magic alongside the usual mechanisms that are compiled together is called a module.

Another (more subtle) observation about the inclusion approach is that non-inline function templates are distinct from inline functions and macros in an important way: They are not expanded at the call site. Instead, when they are instantiated, they create a new copy of a function. Because this is an automatic process, a compiler could end up creating two copies in two different files, and some linkers could even end up with two distinct definitions for the same function. In theory, this should not be a concern of course: It is a problem for the C++ compilation system to accommodate. In practice, things work well most of the time, and we don't need to deal with this issue at all. For large projects that create their own library of code, however, problems occasionally show up. A discussion of instantiation schemes in Chapter 14 and a closer study of the accumulation that comes with a compiler's translation system should help address these problems.

Finally, we need to point out that what applies to the ordinary function template in our example also applies to member functions and static data members of class templates, as well as to member-function templates.

## 9.2 TEMPLATES AND INLINE

Reducing function calls to inline is a common tool to improve the running time of our programs. The `inline` specifier was meant to be a hint for the implementation that inline substitution of the function body at the point of call is preferred over the usual function call mechanism.

However, an implementation may ignore the hint. Hence, the only guaranteed effect of `inline` is to allow a function definition to appear multiple times in a program (usually because it appears in a header file that is included in multiple places).

Using inline functions, function templates can be defined in multiple translation units. This is usually achieved by placing the definition in a header file that is included by multiple C++ files.

This doesn't mean, however, that function templates use inline substitution by default. It is entirely up to the compiler whether or not inline substitution of a function template body at the point of its call is preferred over the usual function call mechanism. Perhaps surprisingly, compilers are often better than programmers at estimating whether inlining a call would lead to a net performance improvement. As a result, the precise policy of a compiler with respect to `inline` is very different from compiler to compiler, and even depends on the options selected for a specific compilation.

Nevertheless, with appropriate performance monitoring, a programmer may have better information than a compiler and may therefore wish to override compiler decisions (e.g., when using software for particular platforms, such as mobile phones, or particular inputs). Sometimes this is only possible with compiler-specific attributes such as `noinline` or `always_inline`.

It's worth pointing out at this point that full specializations of function templates act like ordinary functions in this regard. Their definition can appear only once unless they're defined inline (see Section 16.3 on page 859). See also Appendix A for a broader, detailed overview of this topic.

## 9.3 PRECOMPILED HEADERS

Even without templates, C++ header files can become very large and therefore take a long time to compile. Templates add to this tendency, and therefore many of the waiting programmers have in many cases driven vendors to implement a remedy. Headers like `<iostream>` have the standard library implementation available, although we leave the details on how to create and use precompiled headers.

When a compiler translates a file, it does so starting from the beginning of the file and working through to the end. As it processes each token from the file (which may come from an `#include`d file), it adapts its internal state, including such things as adding entries to a table of symbols so they may be looked up later. While doing so, the compiler may also generate code in object files.

The precompiled header scheme relies on the fact that code can be organized in such a manner that many files start with the same lines of code. Let's assume the use of a precompiled header that every file to be compiled starts with the same N lines of code. We could compile these N lines and save the complete state of the compiler at that point in a precompiled header. Then, for every file in our program, we could reload the saved state and start compiling at line N+1. At this point it is worthwhile to note that reloading the saved state is an operation that can be orders of magnitude faster than actually compiling the first N lines. However, saving the state in the first place is typically more expensive than just compiling the N lines. The increase in cost varies roughly from 20 to 200 percent. as much as possible— files start with a maximum number of common lines of code. In practice this means the files must start with the same `#include` directives, which, as mentioned earlier, consume a substantial portion of our build time. Hence, it can be very advantageous to pay attention to the order in which headers are included. For example, the following two files:

```cpp
#include <vector>
#include <list>

and

#include <list>
#include <vector>
```

inhibit the use of precompiled headers because there is no common initial state in the sources.

Some programmers decide that it is better to `#include` some extra unnecessary headers than to pass on an opportunity to accelerate the translation of a precompiled header. This decision can considerably ease the management of the inclusion policy. For example, it is usually relatively straightforward to create a header file named `stdafx.h` that includes all the standard headers:

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <deque>
#include <list>
```

This file can then be precompiled, and every program file that makes use of the standard library can then simply be started as follows:

```cpp
#include "stdafx.h"
```

Normally this would take a while to compile, but given a system with sufficient memory, the pre-compiled header scheme allows it to be processed significantly faster than almost any single standard header would require without precompilation. The standard headers are particularly convenient in this way because they rarely change, and hence the precompiled header for our stdafx.h file can be built once. Otherwise, precompiled headers are typically part of the dependency configuration of a project (e.g., they are updated as needed by the popular make tool or an integrated development environment (IDE) project build tool).

One attractive approach to manage precompiled headers is to create layout-specific precompiled header files from the most widely used standard headers (e.g., stdafx.h, stdc++ header) to headers that aren't expected to change all the time and therefore are still worth precompiling. However, if headers are under heavy development, creating precompiled headers for them can take more time than what is saved by reusing them. A key concept to this approach is that a precompiled header for a more stable layer can be reused to improve the precompilation time of a less stable header. For example, suppose that in addition to `stdafx.h`, `stdc++ header` (which we have precompiled), we also define a `cow_p.h` header that includes additional facilities that are specific to our project but nonetheless achieve a certain level of stability:

```cpp
#include "stdafx.h"
#include "stdc++ header"
#include "cow_alpha.hpp"
```

Because this file starts with `#include "stdafx.h"`, the compiler can load the associated precompiled-header and continue with the next without recompiling all the standard headers. When the file is completely processed, a new precompiled header can be produced. Applications can then use `#include "cow.h"` to provide access quickly to large amounts of functionality because the compiler can load the latter precompiled header.

## 9.4 DECODING THE ERROR NOVEL

Ordinary compilation errors are normally quite succinct and to the point. For example, when a compiler says `class X has no member 'func'`, it usually isn't too hard to figure out what is wrong in our code (i.e., we must have mistyped an `X::func`). Not so with templates. Let's look at some examples.

### Simple Type Mismatch

Consider the following relatively simple example using the C++ standard library:

*Click here to view code*

buss/cerrormove12.cpp

```cpp
#include <string>

#include <map>

#include <algorithm>

int main()
{

    std::map<std::string,double> coll;

    // find the first nonempty string in coll
```
