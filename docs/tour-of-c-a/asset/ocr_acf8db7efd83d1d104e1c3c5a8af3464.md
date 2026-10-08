```
template <class T>
constexpr T viscosity = 0.4;
```

```
template <class T>
constexpr space_vector<T> external_acceleration = { T{}, T{-9.8}, T{}} };
```

```
auto vis2 = 'viscosity'<double>;
auto acc = external_acceleration<float>;
```

Here, space_vector is a three-dimensional vector.

Curiously enough, most variables seem to be constants. But then, so are many variables. Terminology has not kept up with our notions of immutability.
Naturally, we can use expressions of suitable types as initializers. Consider:

Click here to view code image

```
template<typename T, typename T2>
constexpr bool is_assignable<T,T2>::value; // Is_assignable is a type trait (§16.4.1)
```

```
template<typename T>
void testing() {
    static_assert(Assignable<T,double>, "can't assign a double to a T");
    static_assert(Assignable<T,string>, "can't assign a string to a T");
}
```

After some mutations, this idea becomes the heart of count definitions (§8.2).
The standard library uses variable templates to provide mathematical constants, such as pi and log2 (§17.9).

# 7.4.2 Aliases

Surprisingly often, it is useful to introduce a synonym for a type or a template. For example, the standard header <cstddef> contains the definition of the aliases size_t, maybe:

```
using size_t = unsigned int;
```

The actual type size_t is implementation-dependent, so in another implementation size_t may be an unsigned long. size_t allows the programmer to write portable code. It is very common to provide a parameterized type for aliases related to their template arguments. For example:

```
template<typename T>
class Vector {
public:
    using value_type = T;
    // ...
};
```

In fact, every standard-library container provides value_type as the name for the type of its elements (Chapter 12). This allows us to write code that will work for any container that follows this convention. For example:

Click here to view code image