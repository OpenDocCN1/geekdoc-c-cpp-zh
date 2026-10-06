# ISO/IEC 14882:2017(E)

Table 31 — Allocator requires (continued)

| Expression | Return type | Assertion/note pre/post-condition | Default |
| --- | --- | --- | --- |
| a1 != a2 | bool | same as !(a1 == a2) | |
| a == b | bool | same as a == b Y::rebind<DP>::other(b) | |
| a != b | bool | same as (a == b) Shall not exit via an exception. Postconditions: u == a | |
| X(u); | | | Shall not exit via an exception. Postconditions: Y(u) = b, u == X(b) | |
| X u = a; | | | Shall not exit via an exception. Postconditions: u is equal to the prior value of a. | |
| U(b); | | | Shall not exit via an exception. Postconditions: u is equal to the prior value of X(b). | |
| X(std::move(a)); | | | Shall not exit via an exception. Postconditions: u is equal to the prior value of a. | |
| X(std::move(b)); | | | Shall not exit via an exception. Postconditions: u is equal to the prior value of X(b). | |
| a.construct(c, args) | (not used) | Effects: Construct an object c Type C at c | ::new(void*) C(forward<Args>(args...))
| a.destroy(c) | (not used) | Effects: Destroys the object at c Typically returns an error or X() return a; |
| X::propagate_on_container_copy_assignment | Identical to or derived from_type or false_type | true_type only if an allocator of type X should be copied when the client container copy-assigned. See Note, below. | false_type |
| X::propagate_on_container_move_assignment | Identical to or derived from_type or false_type | true_type only if an allocator of type X should be moved when the client container move-assigned. See Note, below. | false_type |
| X::propagate_on_container_swap | Identical to or derived from_type or false_type | true_type only if an allocator of type X should be swapped when the client container is swapped. See Note, below. | false_type |
| X::is_always_equal | Identical to or derived from_type or false_type | true_type only if the expression is guaranteed to be true for two (possibly) values a1, a2 of type X. | is_same<X>::type |

3 Note: The member class template rebind in the table above is effectively a typedef template. [Note: In general, if the name Allocator is SomeAllocator<T>, then Allocator::rebind<U>::other is the same type as SomeAllocator<T>::value_type is T and SomeAllocator<U>:: |

§ 20.5.3.5

465