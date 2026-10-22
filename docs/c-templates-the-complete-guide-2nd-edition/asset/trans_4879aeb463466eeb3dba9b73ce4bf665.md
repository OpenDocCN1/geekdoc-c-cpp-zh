

```
template<typename T>
  typename std::enable_if<!std::is_lvalue_reference<T>::value>::type
rvalues(T&&);  // accepts rvalues of any type
```

```
template<typename T, unsigned N>
T* begin(T (&array)[N])
{
    return array;
}

template<typename Container>
typename Container::iterator begin(Container& c)
{
    return c.begin();
}

int main()
{
    std::vector<int> v;
    int a[10];

    ::begin(v);  // OK: only container begin() matches, because the first deduction fails
    ::begin(a);  // OK: only array begin() matches, because the second substitution fails
}
```

```
template<typename T> auto f(T p) {
    return p->m;
}

int f(...);

template<typename T> auto g(T p) -> decltype(f(p));

int main()
{
    g(42);
}
```

```
template<typename T>
class B {
};

template<typename T>
class D : public B<T> {
};

template<typename T> void f(B<T>*);

void g(D<long> dl)
{
    f(&dl);  // deduction succeeds with T substituted with long
}
```

```
template<typename T> int f(T, typename T::X);

struct V {
    V();
    struct X {
        X(double);
    };
} v;
int r = f(v, 7.0);  // OK: T is deduced to int through the first parameter,
//      which causes the second parameter to have type V::X
//      which can be constructed from a double value
```

```
```cpp
::max<std::string>(s, "hello")
```
```

```
template<typename T>
class S {
  public:
    S(T b) : a(b) {
    }
  private:
    T a;
};

S x(12); // ERROR before C++17: the class template parameter T was not deduced from
        // the constructor call argument 12
```

```
class S {
    public:
        S(int, int);
};

S s(0, 0);

int main()
{
    init(&s, S(7, 42));  // T() is invalid for T = S, but the default
                         // call argument T() needs no instantiation
                         // because an explicit argument is given
}
```

```
template<typename T>
void f (T x = 42)
{
}

int main()
{
    f<int>(); // OK: T = int
    f();      // ERROR: cannot deduce T from default call argument
}
```

```
template<typename T>
void g(T, int) throw(typename T::Nonexistent);  // #1

template<typename T>
void g(T, ...);                         // #2

void test(int i)
{
    g(i, i);  // ERROR: chooses #1, but the type T::Nonexistent is ill-formed
}
```

```
template<typename T> T default_value()
{
    return T{};
}

int main()
{
    return default_value<int>();
}
```

```
template<Out, typename In>
Out convert(In p)
{
    ...
}

int main() {
    auto x = convert<double>(42);  // the type of parameter p is deduced,
                                   // but the return type is explicitly specified
}
```

```
int f(int);                 // #1
template<typename T> T f(T);   // #2

int main() {
    auto x = f(42);         // calls #1
    auto y = f<>(42);       // calls #2
}
```

```
```cpp
void f();
template<typename> void f();
namespace N {
  class C {
    friend int f();              // OK
    friend int f<>();            // ERROR: return type conflict
  };
}
```
```

```
template<typename T> typename T::EType f();  // #1
template<typename T> T f();                // #2

int main() {
    auto x = f<int*>();
}
```

```
template<typename T> void f(T);
template<typename T> void f(T, T);

int main() {
    auto x = f<int*>;     // ERROR: there are two possible f<int*> here
}
```

```
template<typename ... Ts> void f(Ts ... ps);

int main() {
    f<double, double, int>(1, 2, 3);  // OK: 1 and 2 are converted to double
}
```

```
typename Container::const_iterator pos = container.begin();
...
typename std::iterator_traits<typename Container::iterator>::reference
    element = *pos++;
```

```
template<typename T> void deducePos(T pos);
deducePos(container.begin());
```

```
template<typename T> deduceElement(T& element);
deduceElement(*pos++);
```

```
template<typename t> void f(T&& fr);  // auto replaced by template parameter T
```

```
template<typename Container> void g(Container c) {
    for (auto&& x: c) {
        ...
    }
}
```

```
```cpp
template<typename T> struct X { T const m; };
auto const N = 400u;                    // OK: constant of type unsigned int
auto* gp = (void*)nullptr;              // OK: gp has type void*
auto const S::*pm = &X<int>::*m;        // OK: pm has type int const X<int>::*
X<auto> xa = X<int>();                  // ERROR: auto in template argument
int const auto::*pm2 = &X<int>::m;      // ERROR: auto is part of the “declarator”
```
```

```
int g() {
  auto int r = 24;  // valid in C++03 but invalid in C++11
  return r;
}
```

```
auto lm = [] (int x) { return f(x); };
// same as: [] (int x) -> auto { return f(x); };
```

```
auto f();  // forward declaration
auto f() { return 42; }
```

```
struct S {
    auto f();  // the definition will follow the class definition
};
auto S::f() { return 42; }
```

```
template<typename T, T V> struct S;
S<int, 42>* ps;
```

```
S<3.14>* pd;  // ERROR: floating-point nontype argument
```

```
template<auto V> struct Value {
    using ArgType = decltype(V);
};
```

```
template<typename> struct PMClassT;
template<typename C, typename M> struct PMClassT<M C::*> {
    using Type = C;
};
template<typename PM> using PMClass = typename PMClassT<PM>::Type;

template<auto PMD> struct CounterHandle {
    PMClass<decltype(PMD)>& c;
    CounterHandle(PMClass<decltype(PMD)>& c): c(c) {
    }
    void incr() {
        ++(c.*PMD);
    }
};

struct S {
    int i;
};

int main() {
    S s{41};
    CounterHandle<&S::i> h(s);
    h.incr();  // increases s.i
}
```

```
OldCounterHandle<int S::*, &S::i>
```

```
template<auto... VS> struct Values {
};
Values<1, 2, 3> beginning;
Values<1, 'x', nullptr> triplet;
```

```
template<auto V1, decltype(V1)... VRest> struct HomogeneousValues {
};
```

```
decltype((s))  // check the value category of (s)
```

```
??? f();

decltype(f()) g()
{
    return f();
}
```

```
decltype(*pos) element = *pos;
```

```
std::vector<int> v = { 42 };
auto x = v[0];      // x denotes a new object of type int
decltype(auto) y = v[0];  // y is a reference (type int&)
```

```
decltype(auto) element = *pos;
```

```
```cpp
template<typename C> class Adapt
{
    C container;
    ...
    decltype(auto) operator[] (std::size_t idx) {
        return container[idx];
    }
};
```
```

```
decltype(auto)* p = (void*)nullptr;  // invalid
int const N = 100;
decltype(auto) const NN = N*N;      // invalid
```

```
```cpp
int x;
decltype(auto) z = x;              // object of type int
decltype(auto) r = (x);             // reference of type int&
```
```

```
int g();
...
decltype(auto) f() {
    int r = g();
    return (r);    // run-time ERROR: returns reference to temporary
}
```

```
template<decltype(auto) Val> class S
{
    ...
};
constexpr int c = 42;
extern int v = 42;
S<c> sc;    // #1 produces S<42>
S<(v)> sv;  // #2 produces S<(int&)v>
```

```
template<auto N> struct S {};
template<auto N> int f(S<N> p);
S<42> x;
int r = f(x);
```

```
```cpp
template<auto V> int f(decltype(V) p);
int r1 = deduce<42>(42);   // OK
int r2 = deduce(42);       // ERROR: decltype(V) is a non deduced context
```
```

