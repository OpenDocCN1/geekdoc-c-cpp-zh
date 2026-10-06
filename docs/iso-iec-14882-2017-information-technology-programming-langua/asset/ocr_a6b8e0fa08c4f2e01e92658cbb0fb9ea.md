# ISO/IEC 14882:2017(E)

Table 90 — Associative container requirements (in addition to container) (continued)

| Expression | Return type | Assertion/note pre/post-condition | Complexity |
| a_eq::emplace(args) | iterator | Requires: value_type shall be Emplace-constructible into X from args. Effects: Inserts a value_type object t constructed with std::forward<Args>(args)... and returns the iterator pointing to the newly inserted element. If a range equivalent to a_eq exists at the end of that range | logarithmic |
| a_emplace_hint(p, args) | iterator | equivalent to a::emplace(std::forward<Args>(args)...). Return value is an iterator keying to the newly inserted element. The element is inserted as close as possible to the position just prior to p. | logarithmic in general, but amortized if the element is inserted right before |
| a_uniq::insert(t) | pair<iterator, bool> | Requires: If t is a non-const expression, value_type shall be MoveInsertable into X. Otherwise, value_type shall be Copyable into X. Effects: Inserts t and only if there is no element in the container with key equivalent to the key of t. The bool component of the returned pair is true if and only if the insertion takes place, and the iterator component of the pair points to the element keying to the key of t. | |

§ 26.2.6 ©ISO/IEC 2017 – All rights reserved 845