In the remainder of this chapter, we will explore the implementation and manipulation of the Tuple class template, which is a simplified version of the class template std::tuple.

# 25.1 Basic Tuple Design

# 25.1.1 Storage

Tuples contain storage for each of the types in the template argument list. That storage can be accessed through a function template get, used as get<I>(t) for a tuple t. For example, get<0>(t) on the t in the previous example would return a reference to the int 17, while get<1>(t) returns a reference to the double 3.14.

The recursive formulation of tuple storage is based on the idea that a tuple containing N > 0 elements can be stored as both a single element (the first element, or header of the list) and a tuple containing N − 1 elements (the tail), with a separate special case for a zero-element tuple. Thus, a three-element tuple Tuple<int, double, std::string> can be stored as an int and a Tuple<double, std::string>. That two-element tuple can then be stored as a double and a Tuple<std::string>, which itself can be stored as a std::string and a Tuple<>. In fact, this is the same kind of recursive decomposition used in the generic versions of typelist algorithms, and the actual implementation of recursive tuple storage unfolds similarly: Click here to view code image

```
template<typename... Types>
class Tuple;

// recursive case:
template<typename Head, typename... Tail>
class Tuple<Head, Tail...>
{
private:
Head head;
Tuple<Tail...> tail;
public:
// constructors:
Tuple() {
}
Tuple(Head const& head, Tuple<Tail...> const& tail)
```