```
```cpp
struct X {
static constexpr Point p {100,250}; // Point must be a literal type (§10.4.3)
static const int m1 = 7;
static int m2 = 8; // error : not const

static int m3;
static void f1() { /* ... */ } static void f2();
};
template<typename T> int X<T>::m1 = 88; // error : two initializers
template<typename T> int X<T>::m3 = 99;

template<typename T> void X<T>::f2() { /* ... */ }
```
```

As for non-template classes, a const or constexpr static data member of literal type can be initialized in-class and need not be defined outside the class (§17.4.5, §iso.9.2).

A static member need only be defined if it is used (§iso.3.2, §iso.9.4.2, §16.2.12). For example:

```
```cpp
template<typename T>
struct X {
static int a;
static int b;
};

int * p = &X<int>::a;
```
```

If this is all the mention of X<int> in a program, we will get a “not defined” error for X<int>::a, but not for X<int>::b.

# 23.4.5 Member Types

As for an “ordinary class,” we can define types as members. As usual, such a type can be a class or an enumeration. For example:

```
```cpp
template<typename T>
struct X {
enum E1 { a, b };
enum E2; // error : underlying type not known
enum class E3;
enum E4 : char;

struct C1 { /* ... */ }; struct C2;
};
template<typename T>
enum class X<T>::E3 { a, b }; // needed
template<typename T>
enum class X<T>::E4 : char { x, y }; // needed
template<typename T>
struct X<T>::C2 { /* ... */ }; // needed
```
```