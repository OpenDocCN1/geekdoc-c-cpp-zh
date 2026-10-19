# ISO/IEC 14882:2020(E)

Table 33: Cpp17NullablePointer requirements [tab:cpp17.nullablepointer]

| Expression | Return type | Operational semantics |
|---|---|---|
| P u(np);\nP u = np; |  | Postconditions: u == nullptr |
| P(np) |  | Postconditions: P(np) == nullptr |
| t = np | P& | Postconditions: t == nullptr |
| a != b | contextually convertible to bool | !(a == b) |
| a == np\nnp == a | contextually convertible to bool | a == P() |
| a != np\nnp != a | contextually convertible to bool | !(a == np) |

(1.2) — it meets the Cpp17CopyConstructible (Table 29) and Cpp17Destructible (Table 32) requirements, and

(1.3) — the expressions shown in Table 34 are valid and have the indicated semantics.

2 Given Key is an argument type for function objects of type H, in Table 34 h is a value of type (possibly const) H, u is an lvalue of type Key, and k is a value of a type convertible to (possibly const) Key.

Table 34: Cpp17Hash requirements [tab:cpp17.hash]

| Expression | Return type | Requirement |
|---|---|---|
| h(k) | size_t | The value returned shall depend only on the argument k for the duration of the program.\n[Note 1: Thus all evaluations of the expression h(k) with the same value for k yield the same result for a given execution of the program. — end note]\nFor two different values t1 and t2, the probability that h(t1) and h(t2) compare equal should be very small, approaching 1.0 / numeric_limits<size_t>::max(). |
| h(u) | size_t | Shall not modify u. |

# 16.4.4.6 Cpp17Allocator requirements [allocator.requirements]

# 16.4.4.6.1 General [allocator.requirements.general]

1 The library describes a standard set of requirements for allocators, which are class-type objects that encapsulate the information about an allocation model. This information includes the knowledge of pointer types, the type of their difference, the type of the size of objects in this allocation model, as well as the memory allocation and deallocation primitives for it. All of the string types (Clause 21), containers (Clause 22) (except array), string buffers and string streams (Clause 29), and match_results (Clause 30) are parameterized in terms of allocators.

2 The class template allocator_traits (20.10.9) supplies a uniform interface to all allocator types. Table 35 describes the types manipulated through allocators. Table 36 describes the requirements on allocator types and thus on types used to instantiate allocator_traits. A requirement is optional if the last column of Table 36 specifies a default for a given expression. Within the standard library allocator_traits template, an optional requirement that is not supplied by an allocator is replaced by the specified default expression. A user specialization of allocator_traits may provide different defaults and may provide defaults for different requirements than the primary template. Within Tables 35 and 36, the use of move and forward always refers to std::move and std::forward, respectively.

Table 36: Cpp17Allocator requirements [tab:cpp17.allocator]

| Expression | Return type | Assertion/note pre-/post-condition | Default |
|---|---|---|---|
| X::pointer |  |  | T* |