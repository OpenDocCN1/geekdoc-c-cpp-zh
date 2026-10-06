# ISO/IEC 14882:2017(E)

— end example[]

12 A template-parameter shall not be given default arguments by two different declarations in the same scope.
[Example]:

```cpp
template<class T = int> class X;
template<class T = int> class X { /* ... * / }; // // error
```
— end example[]

13 When parsing a default template-argument for a non-type template-parameter, the first non-nested > is taken
as the end of the template-parameter-list rather than a greater-operator. [Example]:

```cpp
template<int i = 3 > 4>
class X { /* ... * / }; // syntax error
template<int i = (3) > 4>
class Y { /* ... * / }; // OK
```
— end example[]

14 A template-parameter of a template template-parameter is permitted to have a default template-argument.
When such arguments are specified, they apply to the template-parameter in the scope of
the template-parameter.... [Example]:

```cpp
template <class T = float> struct B {};
template <class TT = float> struct A {
inline void f();
inline void g();

template <class TT> T> void A<TT>::f() {
T--; // error TT has no default argument
}
template <class TT = char> T> void A<TT>::g() {
T--; // OK
}
```
— end example[]

15 If a template-parameter is a type-parameter with an ellipsis prior to its optional identifier or is a parameter-
declaration that declares a parameter pack is a pack expansion, then the template-parameter is a template parameter
pack (17.5.3). A template pack that is a parameter-declaration is a pack expansion. Similarly, a parameter pack that is a
type-parameter with a template-parameter-list containing one or more expanded parameter packs is a pack
expansion. A template parameter pack that is a pack expansion will not expand in the same template-parameter-list.... [Example]:

```cpp
template<class...> Types> class Tuple;
// Types is a template type parameter pack
// not a pack expansion
template<class T, int...> struct multi_array;
// Dims is not a non-type template parameter pack
// not a pack expansion
template<class...> T> struct value_holder {
template<T... Values> struct apply {};
};
// Values is a non-type template parameter pack
// and a pack expansion

template<class...> T, T... Values...> struct static_array;
// error: Values expands template type parameter
// pack T within the same template parameter list
```
— end example[]

§ 17.1

©ISO/IEC 2017 – All rights reserved

346