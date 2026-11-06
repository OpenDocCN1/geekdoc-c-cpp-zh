a class template. The class template defines an enum value result which is returned by the function, unless no int values were specified, in which case 0 is returned.

```
~~~
template <int ... Ints>
int forwarder()
{
    return computer<Ints ...>::result;  // forwarding the Ints
}

template <>    // specialization if no ints are provided
int forwarder<>()
{
    return 0;
}

// use as:
cout << forwarder<1, 2, 3>() << ' ' << ' ' << forwarder<>() << '\n';
~~~
```

The sizeof operator can be used for variadic non-type parameters as well: sizeof...(Ints) would return 3 when used in the first function template for forwarder<1, 2, 3>().

Variadic non-type parameters are used to define variadic literal operators, introduced in section 22.3.

# ## 21.6 Tuples (C++11)

The C++11 standard offers a *generalized pair container*: the *tuple*, covered in this section. Before tuples can be used the header file `<tuple>` must have been included.

Whereas `std::pair` containers have limited functionality and only support two members, tuples have slightly more functionality and may contain an unlimited number of different data types. In that respect a tuple can be considered the *template's answer to C's struct*.

A tuple's generic declaration (and definition) uses the variadic template notation:

```
~~~
template <class ...Types>
class tuple;
~~~
```

Here is an example of its use:

```
~~~
typedef std::tuple<int, double &, std::string, char const *> tuple_idsc;

double pi = 3.14;
tuple_idsc idsc(59, pi, "hello", "fixed");

// access a field:
std::get<2>(idsc) = "hello world";
~~~
```

The `std::get<idx>(tupleObject)` function template returns a reference to the idx<sup>th</sup> (zero based) field of the tuple `tupleObject`. The index is specified as the function template's non-type template argument.

Tuples may be constructed without specifying initial values. Primitive types are initialized to zeroes; class type fields are initialized by their default constructors. Be aware that in some situations the construction of a tuple may succeed but its use may fail. Consider:

```
~~~
tuple<int &> empty;
cout << get<0>(empty);
~~~
```