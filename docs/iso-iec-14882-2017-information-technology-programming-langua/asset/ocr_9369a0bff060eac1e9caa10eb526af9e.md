# ISO/IEC 14882:2017(E)

Table 45 — Const-volatile modifications (continued)

| Template | Comments |
|---|---|
| template <class T> struct remove_volatile; | The member typed type names the same type as T except that any top-level volatile-qualifier has been removed. [Example: remove_volatile_t<const int> evaluates to const int, whereas remove_volatile_t<volatile int> evaluates to volatile int — end example] |
| template <class T> struct remove_cv; | The member typed type names the same type as T except that top-cv-qualifier has been removed. [Example: remove_cv_t<const int> evaluates to int, whereas remove_cv_t<volatile int> evaluates to const volatile int — end example] |
| template <class T> struct add_const; | If T is a reference, function, or top-level const-qualified type, then T1; otherwise, type names T. |
| template <class T> struct add_volatile; | If T is a reference, function, or top-level volatile-qualified type, then type names the same type as T, otherwise T volatile. |
| template <class T> struct add_cv; | The member typed type names the same type as add_const_t<add_volatile_t<T>> |

23.15.7.2 Reference modifications [meta.trans.ref]

Table 46 — Reference modifications

| Template | Comments |
|---|---|
| template <class T> struct remove_reference; | If T names a "reference to T1" then the member typed type names T1; otherwise, type names T. |
| template <class T> struct add_lvalue_reference; | If T names a referable type (20.3.18) then the member typed type names T&; otherwise, type T. [Note: This rule reflects the semantics of reference collapsing (11.3.2). — end note] |
| template <class T> struct add_rvalue_reference; | If T names a referable type then the member typed type names T&&; otherwise, type T. [Note: This rule reflects the semantics of reference collapsing (11.3.2). For example, when a T names an add_rvalue_reference<T> is not an rvalue reference. — end note ]

§ 23.15.7.2 ©ISO/IEC 2017 – All rights reserved 69-4