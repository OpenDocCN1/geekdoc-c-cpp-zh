# A.9.4 Anonymous Type Parameters

Starting with the 2011 standard, the SFINAE technique can be applied to template parameter types. This makes the implementations clearly more readable. Function templates are much better structured when the enabling type treatment doesn't distort the return type or an argument but is expressed as an unused and unnamed type parameter. The last example would be accordingly:

```
template <typename T,
         typename= enable_if_t<is_matrix<T>::value
                               && !is_sparse_matrix<T>::value>>
inline Magnitude_t<T> one_norm(const T& A);

template <typename T,
         typename= enable_if_t<is_sparse_matrix<T>::value>>
inline Magnitude_t<T> one_norm(const T& A);
```

As we are now no longer interested in the type defined by enable_if_t, we can take its default for the unused type parameter.

```
=> c++11/enable_if_class.cpp
```

At this point, we want to pick up the topic of controlling the availability of member functions by class template parameters. They are not relevant to SFINAE, and so enable_if expressions are errors. Say we want apply a bitwise AND to each entry of a vector, i.e., implement &= with a scalar. This only makes sense when the vector has integer values:

```
template <typename T>
class vector
{
    ...
    template <typename= enable_if_t<std::is_integral<T>::value>>
    vector<T& operator&=(const T& value); // error
};
```

Unfortunately, this code doesn't compile. The substitution failure must depend on a template parameter of the function and of the class.

According to Jeremiah Wilcock, it only has to seem dependent on a template parameter. Thus, our operator&= must depend on some parameter, say U, so that we can apply enable_if on U:

```
template <typename T>
class vector
{
    template <typename U>
    struct is_int : std::is_integral<T> {};

    template <typename U, typename= enable_if_t<std::is_integral<U>::value> >
    vector<T& operator&=(const U& value);
};
```