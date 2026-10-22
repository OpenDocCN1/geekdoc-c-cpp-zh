```
class PushFrontT<Tuple<Types...>, Element> {
public:
using Type = Tuple<Element, Types...>;
};
```

// add element to the back:

```
template<typename... Types, typename Element>
class PushBackT<Tuple<Types...>, Element> {
public:
using Type = Tuple<Types..., Element>;
};
```

Now, all of the typelist algorithms developed in Chapter 24 work equally well with Tuple and Typelist, so that we easily can deal with the type of tuples. For example: Click here to view code image

```
Tuple<int, double, std::string> t1(17, 3.14, "Hello, World!");
using T2 = PopFront<PushBack<decltype(t1), bool>>;
T2 t2(get<1>(t1), get<2>(t1), true);
std::cout << t2;
```

which prints:

```
(3.14, Hello, World!, 1)
```

As we will see shortly, typelist algorithms applied to tuple types are often used to help determine the result type of a tuple algorithm.

# 25.3.2 Adding to and Removing from a Tuple

For the values of tuples, the ability to add an element to the beginning or end of a tuple is important for building more advanced algorithms. As with typelists, insertion at the front of a tuple is far easier than insertion at the back, so we start with pushFront: Click here to view code image

tuples/pushfront.hpp

```
template<typename... Types, typename V>
PushFront<Tuple<Types...>, V>
pushFront(Tuple<Types...> const& tuple, V const& value)
{
return PushFront<Tuple<Types...>, V>(value, tuple);
}
```

Adding a new element (called value) onto the front of an existing tuple