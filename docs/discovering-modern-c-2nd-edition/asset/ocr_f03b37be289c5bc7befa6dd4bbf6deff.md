```
template <typename T,
typename= enable_if_t<is_matrix<T>::value
&&
!is_sparse_matrix<T>::value >
inline Magnitude<T> one_norm(const T& A);
```

As are now no longer interested in the type defined by `enable_if_t`, we can take its default for the unused type parameter. It has to be mentioned that this form of function enabling doesn't work well for dispatching between multiple implementations.

=> c++11/enable_if_class.cpp

At this point, we want to pick up the topic of controlling the availability of member functions by class template parameters. They are not relevant to SFINAE, and so `enable_if` expressions are errors. Say we want to apply a bitwise AND to each entry of a vector, i.e., implement `&=` with a scalar. This only makes sense when the vector has integer values:

Click here to view code image

```
template <typename T>
class vector
{
    ...
    template <typename=
    enable_if_t<std::is_integral<T>::value> >
    vector<T>& operator&=(const T& value); // error
};
```

Unfortunately, this code doesn't compile. The substitution failure must depend on a template parameter of the function and not of the class. According to Jeremiah Wilcock (one of the `enable_if` inventors), it only has to _seem_ to depend on a function template parameter. Thus, our `operator&=` must depend on some parameter, say U, so that we can apply `enable_if` on U:

Click here to view code image

```
template <typename T>
class vector
{
    template <typename U>
    using is_int = std::is_integral<T>;
    template <typename U, typename=
```