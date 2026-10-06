# ISO/IEC 14882:2017(E)

Table 84 — Reversible container requirements

| Expression | Return type | Assertion/note pre-/post-condition | Complexity |
| --- | --- | --- | --- |
| X::reverse_iterator | iterator type whose type is T | reverse_iterator<T> | compile time |
| X::const_reverse_iterator | constant iterator whose type is T | reverse_iterator<const_> | compile time |
| a.begin() | reverse_iterator; const_reverse_iterator for constant a | reverse_iterator(end()) | constant |
| a.rend() | reverse_iterator; const_reverse_iterator for constant a | reverse_iterator(begin()) | constant |
| a.begin() | const_reverse_iterator | const_cast<const&>(a.begin()) | constant |
| a.rend() | const_reverse_iterator | const_cast<const&>(a.rend()) | constant |

+   11 Unless otherwise specified in 26.2.6.1, 26.2.7.1, 26.3.8.4, and 26.3.11.5 all container types defined in this class must meet the following requirements:

+   (11.1) — if an exception is thrown by an insert() or erase() while inserting a single element, the function has no effects.

+   (11.2) — if an exception is thrown by a push_back(), push_front(), erase_back(), or erase_front(), the function has no effects.

+   (11.3) — no copy constructor or assignment operator of a returned iterator throws an exception.

+   (11.4) — no erase(), clear(), pop_back() or pop_front() throws an exception.

+   (11.5) — no swap() throws an exception.

+   (11.6) — no swap() function invalidates any references, pointers, or iterators referring to the elements of the containers being swapped. [Note: The end() iterator does not refer to any element, so it may be invalidated.— end]

+   12 Unless otherwise specified (either explicitly or by defining a function in terms of other functions), invoking a container member function or passing it as an argument to a library function will invalidate iterators to, or change the values of, objects within that container.

+   13 A contiguous container is a container that supports random access to iterators (27.2.7) and whose member types iterator and const_iterator are contiguous iterators (27.2.1).

+   14 Table 85 lists operations that are provided for some types of containers but not others. Those containers for which the listed operations should implement the semantics described in Table 85 unless otherwise stated.