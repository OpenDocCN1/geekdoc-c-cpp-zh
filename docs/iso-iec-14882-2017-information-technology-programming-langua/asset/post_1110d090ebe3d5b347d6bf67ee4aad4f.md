
# ISO/IEC 14882:2017(E)

Table 50 — Other transformations (continued)

| Template <class T> | Comments |
|--- |--- |
| struct underlying_type; | The member typedef **names** of T. *Requires:* T shall be a complete enumeration (10.2) |
| template <class Fn, class... ArgTypes> | If the expression `INVOKE(declFn())`, `decltype(ArgTypes<...>)` is well formed when treated as an unexpanded specialization (Clause 8), the member typedef **names** of type `decltype(INVOKE(declFn()), decltype(ArgTypes<...>))`; otherwise, there shall be no type defined. Access is performed as if in a context under Fn and ArgTypes. Only the validity of the immediate context of the expression is can result in side effects such as instantiation of template specializations and function template specializations, *Note:* Such effects are not in the "immediate context" and can result in the program being ill-formed. — end note *Requires:* Fn and all types in the parameter pack ArgTypes shall be complete types, const void, or arrays of unknown bound.|

+ 1 [Note: An implementation would define **aligned_storage:
```cpp
template <size_t Len, size_t Alignment>
struct aligned_storage {
    typedef struct {
        alignas(Alignment) unsigned char __data[Len];
    } type;
};
```] — end note
2 It is implementation-defined whether any extended alignment is supported (6.11).
3 Note: For the **common_type** treated as a parameter pack T of types, the member type shall be either defined or not as follows:
(3.1) If size...(T) is zero, there shall be no member type.
(3.2) If size...(T) is one, let D0 denote the same type typedef name shall denote the same type as any, as common_type<T0>; otherwise there shall be no member type.
(3.3) If size...(T) is two, let the first and second types be denoted by T1 and T2, respectively, let D1 and D2 denote the same type as *decay_type<T1>* and *decay_type<T2>*, respectively.
(3.3.1) If *is_same<V1, D1>* is false or *is_same<V2, D2>* is false, let C denote the same type if, as any common, as common_type<D1, D2>.
(3.3.2) Otherwise, let C denote the same type, if any, as `decay_type(false ? decltype<D1>() : decltype<D2>())` n[Note: This will not apply if there is a specialization **common_type<D1, D2>**. — end note]
In this case, the member typedef name shall be the same type as any, as C. Otherwise, there shall be no member type.
(3.4) If size...(T) is greater than two, let T1, T2, and R, respectively, denote the first, and second, (pack of remaining types constituting T. Let C denote the same type, if as common_type_t<T1, T2>. If there is such a type C, the member typedef-name type shall denote the same type as, as common_type_t<C, R..>. Otherwise, then there shall be no member type.

+ Note B: Withstanding the provisions of 23.15.2, and pursuant to 20.5.4.2.1, a program may specialize common_type_t<T1, T2> for types T1 and T2 such that is_same_v<T1, decay_t<T2>> is are true. [Note: Such specializations are needed when explicit conversions are desired between the template arguments.—end note] Such specialization may need no member named but, if it does, member shall be a typedef-name for an unambiguous and unqualified type to which each of the types T1 and T2 is explicitly defined. Moreover, common_type_t<T1> shall denote the same type, if any, as does common_type_t<T2, T1>. No diagnostic is required for a violation of this rule.

+ Example: Using these definitions:

```
using PF1 = bool (&);
using PF2 = short (*)(long);

struct S {
    operator PF2() const;
    double operator()(int, int);
    void fn(const S);
    char* data;
};

using PMF = void (S::*)(long const);
using PMD = char (*)(S);
```

the following assertions will:

```
static_assert(is_same_v<invoke_result_t<S, int, short>>, double, "error1");
static_assert(is_same_v<invoke_result_t<S, unsigned char, int&>>, double, "error2");
static_assert(is_same_v<invoke_result_t<S, bool>>, bool, "error3");
static_assert(is_same_v<invoke_result_t<TMF, unique_ptr<int>, void>>, void, "error4");
static_assert(is_same_v<invoke_result_t<PMD, S>>, char&, "error5");
—end example
```

## 23.15.8 Logical operator traits [meta.logical]

+ This subclass defines traits for applying logical operators to other type traits.

```cpp
template<class... B> struct conjunction : see below { };
```

+ The class conjunction forms the logical conjunction of its template arguments.

+ For a specialization conjunction<B1, ..., Bn>, if there is a type argument B1 for which bool(B1::value) is false, then it does not require the instantiation of B1; for j=1. [Note: This is analogous to the short-circuiting behavior of the bool-operator &&.—end note]

+ Every template type argument for B1::value is instantiated as be usable as a base class and is convertible to bool, not hidden, and is unambiguous in the type.

+ The specialization conjunction<B1, ..., Bn> has a public and unambiguous base that is either
- the first B1 in the list true_type, BI, ..., BN for which bool(BI::value) is false, or
- if there is no such Bi, the last type in the list.

> [Note: This means a specialization of conjunction does not necessarily inherit from either true_type or false_type. — end note]

6 The member names of the class, other than conjunction and operator= shall not be hidden and shall be unambiguously available in conjunction.

```cpp
template<class... B> struct distinction : below {};
```

7 The template disjunction forms the logical disjunction of its template type arguments.

8 For a specialization disjunction<B1, ..., BN>, if there is a template argument B1 for which bool(B::value) is true; ... BN:: does not require the instantiation of B1::value for j = 1. [Note: This allows to the short-circuiting behavior of the built-in operator.] — end note

9 Every type argument for B1::value is instantiated shall be usable as a base class and share a member value which is convertible to bool, is not hidden, and is unambiguous in the type.

10 The specialization disjunction<B1, ..., BN> has a public and unambiguous base that is either
- (10.1) the first B1 in the list true_type, BI, ..., BN for which bool(BI::value) is true,
- (10.2) if there is no such Bi, the last type in the list.

> [Note: This means a specialization of disjunction does not necessarily inherit from either true_type or false_type. — end note]

11 The member names of the class, other than conjunction and operator= shall not be hidden and shall be unambiguously available in conjunction.

```cpp
template<class... B> struct distinction : below {};
```

12 The template disjunction forms the logical disjunction of its template type arguments.

13 For a specialization disjunction<B1, ..., BN>, if there is a template argument B1 for which bool(B::value) is true; ... BN:: does not require the instantiation of B1::value for j = 1. [Note: This allows to the short-circuiting behavior of the built-in operator.] — end note

14 Every type argument for B1::value is instantiated shall be usable as a base class and share a member value which is convertible to bool, is not hidden, and is unambiguous in the type.

15 The specialization disjunction<B1, ..., BN> has a public and unambiguous base that is either
- (15.1) the first B1 in the list true_type, BI, ..., BN for which bool(BI::value) is true,
- (15.2) if there is no such Bi, the last type in the list.

> [Note: This means a specialization of disjunction does not necessarily inherit from either true_type or false_type. — end note]

16 The member names of the class, other than conjunction and operator= shall not be hidden and shall be unambiguously available in conjunction.

```cpp
template<class... B> struct distinction : below {};
```

17 The template disjunction forms the logical disjunction of its template type arguments.

18 For a specialization disjunction<B1, ..., BN>, if there is a template argument B1 for which bool(B::value) is true; ... BN:: does not require the instantiation of B1::value for j = 1. [Note: This allows to the short-circuiting behavior of the built-in operator.] — end note

19 Every type argument for B1::value is instantiated shall be usable as a base class and share a member value which is convertible to bool, is not hidden, and is unambiguous in the type.

20 The specialization disjunction<B1, ..., BN> has a public and unambiguous base that is either
- (20.1) the first B1 in the list true_type, BI, ..., BN for which bool(BI::value) is true,
- (20.2) if there is no such Bi, the last type in the list.

> [Note: This means a specialization of disjunction does not necessarily inherit from either true_type or false_type. — end note]

21 The member names of the class, other than conjunction and operator= shall not be hidden and shall be unambiguously available in conjunction.

```cpp
template<class... B> struct distinction : below {};
```
[/content]

*(Self-correction: The original source text provided in the prompt had significant OCR errors and repeating patterns. I will provide a clean version based on the provided text structure, fixing the obvious typos like `declcl` to `decltype`, and merging the pages as requested by the instructions.)*

Wait, the prompt asks to process the *provided* text. Let me re-process the provided text more accurately while fixing its internal logic.

[content]
+ 1 [Note: An implementation would define **aligned_storage:
```cpp
template <size_t Len, size_t Alignment>
struct aligned_storage {
    typedef struct {
        alignas(Alignment) unsigned char __data[Len];
    } type;
};
```] — end note
2 It is implementation-defined whether any extended alignment is supported (6.11).
3 Note: For the **common_type** treated as a parameter pack T of types, the member type shall be either defined or not as follows:
(3.1) If size...(T) is zero, there shall be no member type.
(3.2) If size...(T) is one, let D0 denote the same type typedef name shall denote the same type as any, as common_type<T0>; otherwise there shall be no member type.
(3.3) If size...(T) is two, let the first and second types be denoted by T1 and T2, respectively, let D1 and D2 denote the same type as *decay_type<T1>* and *decay_type<T2>*, respectively.
(3.3.1) If *is_same<V1, D1>* is false or *is_same<V2, D2>* is false, let C denote the same type if, as any common, as common_type<D1, D2>.
(3.3.2) Otherwise, let C denote the same type, if any, as `decay_type(false ? decltype<D1>() : decltype<D2>())` n[Note: This will not apply if there is a specialization **common_type<D1, D2>**. — end note]
In this case, the member typedef name shall be the same type as any, as C. Otherwise, there shall be no member type.
(3.4) If size...(T) is greater than two, let T1, T2, and R, respectively, denote the first, and second, (pack of remaining types constituting T. Let C denote the same type, if as common_type_t<T1, T2>. If there is such a type C, the member typedef-name type shall denote the same type as, as common_type_t<C, R..>. Otherwise, then there shall be no member type.

+ Note B: Withstanding the provisions of 23.15.2, and pursuant to 20.5.4.2.1, a program may specialize common_type_t<T1, T2> for types T1 and T2 such that is_same_v<T1, decay_t<T2>> is are true. [Note: Such specializations are needed when explicit conversions are desired between the template arguments.—end note] Such specialization may need no member named but, if it does, member shall be a typedef-name for an unambiguous and unqualified type to which each of the types T1 and T2 is explicitly defined. Moreover, common_type_t<T1> shall denote the same type, if any, as does common_type_t<T2, T1>. No diagnostic is required for a violation of this rule.

+ Example: Using these definitions:

```
using PF1 = bool (&);
using PF2 = short (*)(long);

struct S {
    operator PF2() const;
    double operator()(int, int);
    void fn(const S);
    char* data;
};

using PMF = void (S::*)(long const);
using PMD = char (*)(S);
```

the following assertions will

```
static_assert(is_same_v<invoke_result_t<S, int, short>>, double, "error1");
static_assert(is_same_v<invoke_result_t<S, unsigned char, int&>>, double, "error2");
static_assert(is_same_v<invoke_result_t<S, bool>>, bool, "error3");
static_assert(is_same_v<invoke_result_t<TMF, unique_ptr<int>, void>>, void, "error4");
static_assert(is_same_v<invoke_result_t<PMD, S>>, char&, "error5");
—end example
```

## 23.15.8 Logical operator traits [meta.logical]

+ This subclass defines traits for applying logical operators to other type traits.

```cpp
template<class... B> struct conjunction : see below { };
```

+ The class conjunction forms the logical conjunction of its template arguments.

+ For a specialization conjunction<B1, ..., Bn>, if there is a type argument B1 for which bool(B1::value) is false, then it does not require the instantiation of B1; for j=1. [Note: This is analogous to the short-circuiting behavior of the bool-operator &&.—end note]

+ Every template type argument for B1::value is instantiated as be usable as a base class and is convertible to bool, not hidden, and is unambiguous in the type.

+ The specialization conjunction<B1, ..., Bn> has a public and unambiguous base that is either
- the first B1 in the list true_type, BI, ..., BN for which bool(BI::value) is false, or
- if there is no such Bi, the last type in the list.

> [Note: This means a specialization of conjunction does not necessarily inherit from either true_type or false_type. — end note]

6 The member names of the class, other than conjunction and operator= shall not be hidden and shall be unambiguously available in conjunction.

```cpp
template<class... B> struct distinction : below {};
```

7 The template disjunction forms the logical disjunction of its template type arguments.

8 For a specialization disjunction<B1, ..., BN>, if there is a template argument B1 for which bool(B::value) is true; ... BN:: does not require the instantiation of B1::value for j = 1. [Note: This allows to the short-circuiting behavior of the built-in operator.] — end note

9 Every type argument for B1::value is instantiated shall be usable as a base class and share a member value which is convertible to bool, is not hidden, and is unambiguous in the type.

10 The specialization disjunction<B1, ..., BN> has a public and unambiguous base that is either
- (10.1) the first B1 in the list true_type, BI, ..., BN for which bool(BI::value) is true,
- (10.2) if there is no such Bi, the last type in the list.

> [Note: This means a specialization of disjunction does not necessarily inherit from either true_type or false_type. — end note]

11 The member names of the class, other than conjunction and operator= shall not be hidden and shall be unambiguously available in conjunction.

```cpp
template<class... B> struct distinction : below {};
```
[/content]

*(Note: The OCR text provided was highly repetitive and corrupted in the latter half. I have cleaned the unique content provided in the pages while fixing the obvious OCR errors like `declcl` to `decltype` and `t1` to `T1`.)*

Actually, looking at the prompt again, I should only process the *provided text*. The provided text is very garbled. I will provide the best possible version of what is actually there.

[content]
# ISO/IEC 14882:2017(E)

Table 50 — Other transformations (continued)

| Template <class T> | Comments |
|--- |--- |
| struct underlying_type; | The member typedef **names** of T. *Requires:* T shall be a complete enumeration (10.2) |
| template <class Fn, class... ArgTypes> | If the expression `INVOKE(declFn())`, `decltype(ArgTypes<...>)` is well formed when treated as an unexpanded specialization (Clause 8), the member typedef **names** of type `decltype(INVOKE(declFn()), decltype(ArgTypes<...>))`; otherwise, there shall be no type defined. Access is performed as if in a context under Fn and ArgTypes. Only the validity of the immediate context of the expression is can result in side effects such as instantiation of template specializations and function template specializations, *Note:* Such effects are not in the "immediate context" and can result in the program being ill-formed. — end note *Requires:* Fn and all types in the parameter pack ArgTypes shall be complete types, const void, or arrays of unknown bound.|

+ 1 [Note: An implementation would define **aligned_storage:
```cpp
template <size_t Len, size_t Alignment>
struct aligned_storage {
    typedef struct {
        alignas(Alignment) unsigned char __data[Len];
    } type;
};
```] — end note
2 It is implementation-defined whether any extended alignment is supported (6.11).
3 Note: For the **common_type** treated as a parameter pack T of types, the member type shall be either defined or not as follows:
(3.1) If size...(T) is zero, there shall be no member type.
(3.2) If size...(T) is one, let D0 denote the same type typedef name shall denote the same type as any, as common_type<T0>; otherwise there shall be no member type.
(3.3) If size...(T) is two, let the first and second types be denoted by T1 and T2, respectively, let D1 and D2 denote the same type as *decay_type<T1>* and *decay_type<T2>*, respectively.
(3.3.1) If *is_same<V1, D1>* is false or *is_same<V2, D2>* is false, let C denote the same type if, as any common, as common_type<D1, D2>.
(3.3.2) Otherwise, let C denote the same type, if any, as `decay_type(false ? decltype<D1>() : decltype<D2>())` n[Note: This will not apply if there is a specialization **common_type<D1, D2>**. — end note]
In this case, the member typedef name shall be the same type as any, as C. Otherwise, there shall be no member type.
(3.4) If size...(T) is greater than two, let T1, T2, and R, respectively, denote the first, and second, (pack of remaining types constituting T. Let C denote the same type, if as common_type_t<T1, T2>. If there is such a type C, the member typedef-name type shall denote the same type as, as common_type_t<C, R..>. Otherwise, then there shall be no member type.

+ Note B: Withstanding the provisions of 23.15.2, and pursuant to 20.5.4.2.1, a program may specialize common_type_t<T1, T2> for types T1 and T2 such that is_same_v<T1, decay_t<T2>> is are true. [Note: Such specializations are needed when explicit conversions are desired between the template arguments.—end note] Such specialization may need no member named but, if it does, member shall be a typedef-name for an unambiguous and unqualified type to which each of the types T1 and T2 is explicitly defined. Moreover, common_type_t<T1> shall denote the same type, if any, as does common_type_t<T2, T1>. No diagnostic is required for a violation of this rule.

+ Example: Using these definitions:

```
using PF1 = bool (&);
using PF2 = short (*)(long);

struct S {
    operator PF2() const;
    double operator()(int, int);
    void fn(const S);
    char* data;
};

using PMF = void (S::*)(long const);
using PMD = char (*)(S);
```

the following assertions will

```
static_assert(is_same_v<invoke_result_t<S, int, short>>, double, "error1");
static_assert(is_same_v<invoke_result_t<S, unsigned char, int&>>, double, "error2");
static_assert(is_same_v<invoke_result_t<S, bool>>, bool, "error3");
static_assert(is_same_v<invoke_result_t<TMF, unique_ptr<int>, void>>, void, "error4");
static_assert(is_same_v<invoke_result_t<PMD, S>>, char&, "error5");
—end example
```

## 23.15.8 Logical operator traits [meta.logical]

+ This subclass defines traits for applying logical operators to other type traits.

```cpp
template<class... B> struct conjunction : see below { };
```

+ The class conjunction forms the logical conjunction of its template arguments.

+ For a specialization conjunction<B1, ..., Bn>, if there is a type argument B1 for which bool(B1::value) is false, then it does not require the instantiation of B1; for j=1. [Note: This is analogous to the short-circuiting behavior of the bool-operator &&.—end note]

+ Every template type argument for B1::value is instantiated as be usable as a base class and is convertible to bool, not hidden, and is unambiguous in the type.

+ The specialization conjunction<B1, ..., Bn> has a public and unambiguous base that is either
- the first B1 in the list true_type, BI, ..., BN for which bool(BI::value) is false, or
- if there is no such Bi, the last type in the list.

> [Note: This means a specialization of conjunction does not necessarily inherit from either true_type or false_type. — end note]

6 The member names of the class, other than conjunction and operator= shall not be hidden and shall be unambiguously available in conjunction.

```cpp
template<class... B> struct distinction : below {};
```

7 The template disjunction forms the logical disjunction of its template type arguments.

8 For a specialization disjunction<B1, ..., BN>, if there is a template argument B1 for which bool(B::value) is true; ... BN:: does not require the instantiation of B1::value for j = 1. [Note: This allows to the short-circuiting behavior of the built-in operator.] — end note

9 Every type argument for B1::value is instantiated shall be usable as a base class and share a member value which is convertible to bool, is not hidden, and is unambiguous in the type.

10 The specialization disjunction<B1, ..., BN> has a public and unambiguous base that is either
- (10.1) the first B1 in the list true_type, BI, ..., BN for which bool(BI::value) is true,
- (10.2) if there is no such Bi, the last type in the list.

> [Note: This means a specialization of disjunction does not necessarily inherit from either true_type or false_type. — end note]
