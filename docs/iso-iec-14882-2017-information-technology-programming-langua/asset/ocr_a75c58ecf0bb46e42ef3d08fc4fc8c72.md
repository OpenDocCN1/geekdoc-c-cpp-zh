# ISO/IEC 14882:2017(E)

Table 90 — Associative container requirements (in addition to
container) (continued)

| Expression | Return type | Assertion/note pre/post-condition | Complexity |
|---|---|---|--|
| a_eq. insert(t) | iterator | *Requires:* If t is a non-constant expression, value_type shall be MoveInsertable into X; otherwise, value_type shall be Copyable into X. *Effects:* Insert returns the iterator pointing to the newly inserted element. If a range containing elements equivalent to t exists in a_eq t is inserted at the end of that range | logarithmic |
| a.insert(p, t) | iterator | *Requires:* If p is a non-constant expression, value_type shall be MoveInsertable into X; otherwise, value_type shall be Copyable into X. *Effects:* Insert t if and only if there is no element with key equivalent to the key of t in containers with unique keys inserts t in containers with unique keys always returns the iterator pointing to the element with key equivalent to the key of t, t is inserted as close as possible to the position just prior to p | logarithmic in general, but amortized constant right before p |
| a.insert(i, j) | void | *Requires:* Value_type shall be PlaceConstructible into X from * *Requires:* i, j are not iterators to insert into each element from the range [i, j) if and only if there is no element with key equivalent to the key of that element in containers with unique keys always inserts that element in containers with equivalent keys. | N log(a.size())+ N), where N has the value distance(i, j) |
| a.insert(il) | void | equivalent to a.insert(il.begin(), il.end()) | |

§ 26.2.6 ©ISO/IEC 2017 – All rights reserved 846