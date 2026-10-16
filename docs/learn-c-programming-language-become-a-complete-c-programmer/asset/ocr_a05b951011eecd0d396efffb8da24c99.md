To get that, we need some language lawyering and for now, we have to make do with get<2>(x).

# 28.5.2.1 const Tuples

As defined, get() works for nonconst Tuple elements and can be used on the left-hand side of assignments. For example:

```
Tuple<double , int, char> x {1.1, 42, ‘a’};
get<2>(x) = ‘b’; // OK
```

However, it can’t be used for consts:

```
const Tuple<double , int, char> xx {1.1, 42, ‘a’};
get<2>(xx) = ‘b’; // error :xx is const
char cc = get<2>(xx); // error :xx is const (surprise?)
```

The problem is that get() takes its argument by nonconst reference. But xx is a const, so it is not an acceptable argument.

Naturally, we also want to be able to have const Tuples. For example:

```
const Tuple<double , int, char> xx {1.1, 422, ‘a’}; char cc = get<2>(xx);
cout << “xx: ” << xx << “\n”; get<2>(xx) = ‘x’;
```

```
// OK: reading from const
// error :xx is const
```

To handle const Tuples, we have to add const versions of get() and getNth’s get(). For example:

```
template<typename Ret, int N>
struct getNth { // getNth() remembers the type (Ret) of the Nth element
template<typename T>
static Ret& get(T& t) // get the value element N from t’sBase
{
return getNth<Ret,N-1>::get(*t.base());
}

template<typename T>
static const Ret& get(const T& t) // get the value element N from t’sBase {
return getNth<Ret,N-1>::get(*t.base()); }
};
```

```
template<typename Ret>
struct getNth<Ret,0> {
template<typename T> static Ret& get(T& t) { return t.x; }
template<typename T> static const Ret& get(const T& t) { return t.x; }};
```

```
template<int N, typename T1, typename T2, typename T3, typename T4> Select<N, T1, T2, T3, T4>& get(Tuple<T1, T2, T3, T4>& t)
{
return getNth<Select<N, T1, T2, T3, T4>,N>::get(t); }
```

```
template<int N, typename T1, typename T2, typename T3> const Select<N, T1, T2, T3>& get(const Tuple<T1, T2, T3>& t) {
```