# 23 • Class Templates 755

A template parameter can be mixed with ordinary parameters. For example, let's change the declara- of C:

```
template <typename T> class Test, typename X, typename Y> class C
{
  ...
  Test<X> t1;
  Test<Y> t2;
};
```

Thus, those that are used for the t1 and t2 objects become generic. Of course, we should change the declaration of C to:

```
C<A, int, double> c;
```

The Test will be replaced with A, X with int, and Y with double.

# Default Parameter Values

In a class template we can specify default values for its parameters. For example:

```
template <typename T1, typename T2 = int> class Group {...}
```

It works similar to the default values for function parameters. If we omit the type of T2 and write Group<double> g; the type of T2 will be int. A class template provides default values for all parameters and we want to use all of them when we use empty <>. For example:

```
template <typename T1> string, typename T2 = int> class Group {...}
```

If we write Group<int>; the type of T1 will be string and the type of T2 will be int. We can also specify default values for non-type parameters. For example:

```
template <typename T, int s = 20> class Grades {...}
```

If we write Grades<int>; the type of T will be int and s equal to 20.

# Static Members

A class template can contain static members. Be careful though, each version of the class contains its static members. For example:

```
#include <iostream> // Example 23.7

template <typename T> class A
public:
  A() {cnt++;}
  static inline int cnt = 0; // Since C++17.
  static int f() {return cnt;}
};

int main()
{
  A<int> a1, a2, a3;
  A<double> d1, d2;
```