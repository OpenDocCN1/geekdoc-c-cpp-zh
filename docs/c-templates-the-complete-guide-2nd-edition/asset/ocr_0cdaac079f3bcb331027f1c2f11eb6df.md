Consider the following recursive template: Click here to view code image

```
template<typename T, typename U>
struct Doublify {
};

template<int N>
struct Trouble {
using LongType = Doublify<typename Trouble<N-1>::LongType,
typename Trouble<N-1>::LongType>;
};
template<>
struct Trouble<0> {
using LongType = double;
};

Trouble<10>::LongType ouch;
```

The use of Trouble<10>::LongType not only triggers the recursive instantiation of Trouble<9>, Trouble<8>, ..., Trouble<0>, but it also instantiates Doublify over increasingly complex types. Table 23.1 illustrates how quickly it grows.

| Type Alias | Underlying Type |
|---|---|
| Trouble<0>::LongType | double |
| Trouble<1>::LongType | Doublify<double, double> |
| Trouble<2>::LongType | Doublify<Doublify<double, double>, Doublify<double, double>> |
| Trouble<3>::LongType | Doublify<Doublify<Doublify<double, Doublify<double, double>>, <Doublify<double, double>, Doublify<double, double>>>> |

Table 23.1. Growth of Trouble<N>::LongType

As can be seen from Table 23.1, the complexity of the type description of the expression Trouble<N>::LongType grows exponentially with N. In general, such a situation stresses a C++ compiler even more than do recursive instantiations that do not involve recursive template arguments. One of the problems here is that a compiler keeps a representation of the mangled name for the type. This mangled name encodes the exact template specialization in some way, and early C++ implementations used an encoding that is roughly proportional to the length of the template-id. These compilers then used well