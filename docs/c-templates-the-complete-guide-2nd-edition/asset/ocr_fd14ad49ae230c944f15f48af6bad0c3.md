the return type). However, this would put an extra burden on all users of our template: They would have to specify an extra type in every invocation of our template. In our example, we may therefore need to write the following: accum<int>(name,name+5) This is not an excessive constraint, but it can be avoided.

An alternative approach to the extra parameter is to create an association between each type T for which accum() is called and the corresponding type that should be used to hold the accumulated value. This association could be considered characteristic of the type T, and therefore the type in which the sum is computed is sometimes called a trait of T. As is turns out, our association can be encoded as specializations of a template: Click here to view code image

# traits/accumtraits2.hpp

```
template<typename T>
struct AccumulationTraits;

template<>
struct AccumulationTraits<char> {
using AccT = int;
};

template<>
struct AccumulationTraits<short> {
using AccT = int;
};

template<>
struct AccumulationTraits<int> {
using AccT = long;
};

template<>
struct AccumulationTraits<unsigned int> {
using AccT = unsigned long;
};

template<>
struct AccumulationTraits<float> {
using AccT = double;
};
```

The template AccumulationTraits is called a traits template because it holds a trait of its parameter type. (In general, there could be more than one trait and more than one parameter.) We chose not to provide a generic definition of this template because there isn’t a great way to select a good accumulation type