`p=op(b,e,x)` op does something to the range `[b:e)` and `x`, returning `p`; `foo(x)` foo does something to `x` but returns no result  
`bar(b,e,x)` Does `x` have something to do with `[b:e)`?

I try to be mnemonic when choosing identifiers, so **b** and **e** will be iterators specifying a range, **p** a pointer or an iterator, and **x** some value, all depending on context. In this notation, only the commentary distinguishes no result from a Boolean result, so you can confuse those if you try hard enough. For an operation returning a Boolean, the explanation usually ends with a question mark. Where an algorithm follows the usual pattern of returning the end of an input sequence to indicate “failure,” “not found,” etc. (§4.5.1, §33.1.1), I do not mention that explicitly.

Usually, such an abbreviated description is accompanied with a reference to the ISO C++ standard, some further explanation, and examples.

# 30.2 Headers

The facilities of the standard library are defined in the **std** namespace and presented as a set of headers. The headers identify the major parts of the library. Thus, listing them gives an overview of the library.

The rest of this subsection is a list of headers grouped by function, accompanied by brief explanations and annotated by references to where they are discussed. The grouping is chosen to match the organization of the standard.

A standard header with a name starting with the letter **c** is equivalent to a header in the C standard library. For every header `<X.h>` defining part of the C standard library in the global namespace and also in namespace **std**, there is a header `<cX>` defining the same names. Ideally, the names from a `<cX>` header do not pollute the global namespace (§15.2.4), but unfortunately (due to complexities of maintaining multilanguage, multi-operating-system environments) most do.

# Containers

+   - `<vector>` One-dimensional resizable array §31.4.2
+   - `<deque>` Double-ended queue §31.4.2
+   - `<forward_list>` Singly-linked list §31.4.2
+   - `<list>` Doubly-linked list §31.4.2
+   - `<map>` Associative array §31.4.3
+   - `<set>` Set §31.4.3
+   - `<unordered_map>` `<unordered_set>` Hashed associative array §31.4.3.2 Hashed set §31.4.3.2
+   - `<queue>` Queue §31.5.2
+   - `<stack>` Stack §31.5.1
+   - `<array>` One-dimensional fixed-size array §34.2.1
+   - `<bitset>` Array of bool §34.2.2

The associative containers **multimap** and **multiset** can be found in `<map>` and `<set>`, respectively. The **priority_queue** (§31.5.3) is declared in `<queue>`.

# General Utilities

`<utility>` Operators and pairs §35.5, §34.2.4.1  `<tuple>` Tuples §34.2.4.2  `<type_traits>`