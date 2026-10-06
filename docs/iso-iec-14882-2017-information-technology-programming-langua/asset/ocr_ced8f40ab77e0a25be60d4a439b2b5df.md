# ISO/IEC 14882:2017(E)

Table 30 — Descriptive variable definitions (continued)

| Variable | Definition |
|--- |--- |
| y | a value of type XX::const_void_pointer obtained by conversion from a result of YY::allocate, or else a value of type (possibly const) std::nullptr_t. |
| n | a value of type XX::size_type. |
| Args | a template pack |
| args | a function parameter pack with the pattern Args&& |

Table 31 — Allocator requirements

| Expression | Return type | Assertion/note/post-condition | Default |
|--- |--- |--- |--- |
| X::pointer_ | | X::pointer is convertible to X::const_pointer | pointer_->traits<X::>::rebind<const T> |
| X::void_pointer | | X::pointer is convertible to X::void_pointer. | pointer_->traits<X::>::rebind<const void_t> |
| Y::void_pointer | | X::void_pointer and Y::const_pointer are the same type. | |
| X::const_void_ | | X::pointer. X::const_pointer, and X::const_void_pointer. Y::const_pointer are convertible to X::const_void_pointer. X::const_void_pointer and Y::const_pointer are the same type. | pointer_->traits<X::>::rebind<const void_t> |
| pointer | | | |
| X::const_void_ | | | |
| pointer | | Identical to T | | |
| X::size_type | unsigned integer type | a type that can represent the size of the largest object in the allocation model. | make_unsigned_t_type |
| X::difference_type | signed integer type | a type that can represent the difference between any two pointers in the allocation model. | pointer_->traits<X::>::pointer_->difference_type |
| typename | Y | For all U (including T), Y::template | See Note A, below. |
| X::template | | rebind<U>::other is rebind<T>::other is X. | |
| *p | T& | | |

§ 20.5.3.5 ©ISO/IEC 2017 – All rights reserved 463