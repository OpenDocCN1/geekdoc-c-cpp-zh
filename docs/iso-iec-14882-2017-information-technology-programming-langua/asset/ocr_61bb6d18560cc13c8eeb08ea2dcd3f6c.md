# ISO/IEC 14882:2017(E)

Table 42 — Type properties predicates (continued)

| Template | Condition | Preconditions |
|---|---|---|
| template <T, class... Args> struct is_trivially_constructible; | is_constructible_v<T, Args...> is true and the variable for is_constructible, as defined below, is known to call no operation that is not trivial (6.9,15). | T and all types in the parameter Args shall be complete types, cv void, or arrays of unknown bound. |
| template <T> struct is_trivially_default_constructible; | is_trivially_construct<v> is true. | T shall be a complete type, cv void, or an array of unknown bound. |
| template <T> struct is_trivially_move_constructible; | For a reference type T, the same result as is_trivially_construct<vT, const>, otherwise false. | T shall be a complete type, cv void, or an array of unknown bound. |
| template <T> struct is_trivially_copy_constructible; | For a reference type T, the same result as is_trivially_construct<vT,&&>, otherwise false. | T shall be a complete type, cv void, or an array of unknown bound. |
| template <T, class U> struct is_trivially_assignable; | is_assignable<vT, U> is true, as defined by is_assignable, is known to call no operation that is not trivial (6.9, 15). | T and U shall be complete types, cv void, or arrays of unknown bound. |
| template <T> struct is_trivially_copy_assignable; | For a reference type T, the same result as is_trivially_assignable<vT,&&>, otherwise false. | T shall be a complete type, cv void, or an array of unknown bound. |
| template <T> struct is_trivially_move_assignable; | For a reference type T, the same result as is_trivially_assignable<vT,&&>, otherwise false. | T shall be a complete type, cv void, or an array of unknown bound. |
| template <T> struct is_trivially_destructible; | is_destructible<vT> is true and the indicated destructor is known to be trivial. | T shall be a complete type, cv void, or an array of unknown bound. |