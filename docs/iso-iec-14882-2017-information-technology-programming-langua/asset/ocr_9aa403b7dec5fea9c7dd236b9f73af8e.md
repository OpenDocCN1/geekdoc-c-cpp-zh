# ISO/IEC 14882:2017(E)

Table 96 — Output iterator requirements (in addition to Iterator)
(continued)

| Expression | Return type | Operational semantics | Assertion/note pre/post-condition |
| --- | --- | --- | --- |
| *r++ = o | result is not used | | Remarks: After this operation r is not required to be dereferenced. Postconditions: r is incrementable. |

[Note: The only use of an operator* is on the left side of the assignment statement. Assignment through the value of the iterator happens only once. Algorithms on output iterators should never attempt to pass through the iterator twice. They should be single pass algorithms. Equality and inequality might not be defined. Algorithms that take output iterators can be used with ostreams as the destination for placing data through the stream_iterator class as well as insert iterators and insert pointers. — end note]

# 27.2.5 Forward iterators [forward.iterators]

+   - A class post type X satisfies the requirements of an input iterator (27.2.3),
- X satisfies the DefaultConstructible requirements (20.5.3.1).
- If X is a mutable iterator, reference is a reference to T; if X is a constant iterator, reference is a reference to const.
- the expressions in Table 97 are valid and have the indicated semantics, and
- objects of type X provide the multi-pass guarantee, described.

The domain of == for forward iterators is that of iterators over the same underlying sequence. However, value-initialized iterators may be compared and shall compare equal to other value-initialized iterators of the same type. [Note: Value-initialized iterators may behave as if they reach the end of the same sequence. — end note]

Two dereferenceable iterators a and b of type X offer the multi-pass guarantee if:

+   - a == b implies ++a
- X is a pointer or the expression (void*)++a, * is equivalent to the expression *a.

[Note: The requirement that a == b implies ++ (which is not true for input and output iterators) and the removal of the restrictions on the number of assignments through a mutable iterator (which applies to output iterators) allows the use of multi-pass one-directional algorithms with forward iterators. — end note]

Table 97 — Forward iterator requirements (in addition to iterator)

| Expression | Return type | Operational semantics | Assertion/note pre/post-condition |
| --- | --- | --- | --- |
| r++ | convertible to const T& | { T tmp = r; ++r; return tmp; } |

§ 27.2.5 ©ISO/IEC 2017 – All rights reserved 956