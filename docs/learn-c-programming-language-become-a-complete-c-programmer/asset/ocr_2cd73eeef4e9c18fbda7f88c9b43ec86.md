This function presumably returns the value of the nth element of a container of type C. Because C has to be deduced from an actual argument of get_nth() in a call, conversions are not applicable to the first argument. However, the second argument is perfectly ordinary, so the full range of possible conversions is considered. For example:

```
struct Index {
operator int(); // ...
};

void f(vector<int>& v, short s, Index i) {
int i1 = get_nth<int>(v,2); // exact match
int i2 = get_nth<int>(v,s); // standard conversion: shorttoint
int i3 = get_nth<int>(v,i); // user-defined conversion: Indextoint
}
```

This notation is sometimes called explicit specialization (§23.5.1).

# 23.6 Template Aliases

We can define an alias for a type with the using syntax or with the typedef syntax (§6.5). The using syntax is more general in the important sense that it can be used to define an alias for a template with some of its arguments bound. Consider:

```
template<typename T, typename Allocator = allocator<T>> vector;
using Cvec = vector<char>; // both arguments are bound
Cvec vc = {'a', 'b', 'c'}; // vc is a vector<char,allocator<char>>
template<typename T>
using Vec = vector<T,My_alloc<T>>; // vector using myallocator (2nd argument is bound)
Vec<int> fib = {0, 1, 1, 2, 3, 5, 8, 13}; // fib is a vector<int,My_alloc<int>>
```

In general, if we bind all arguments of a template, we get a type, but if we bind only some, we get a template. Note that what we get from using in an alias definition is always an alias. That is, when we use the alias, it is completely equivalent to a use of the original template. For example:

```
vector<char,alloc<char>> vc2 = vc; // vc2 and vc are of the same type
vector<int,My_alloc<int>> verbose = fib; // verbose and fib are of the same type
```

The equivalence of the alias and the original template implies that if you specialize the template, you (correctly) get the specializations when you use the alias. For example:

```
template<int>
struct int_exact_traits { // idea: int_exact_traits<N>::type is a type with exactly N bits
using type = int;
};

template<>
struct int_exact_traits<8> { using type = char;
};
```