```
~~~cpp
    find(input.begin(), input.end(), string("*bonus"));
if (want != input.end())
{
    vector<string>::reference r = *want;
    r = "bogus";
}
~~~
```

This code makes `r` a reference to the element in `input` to which `want` points. Similarly, continuing with the preceding example, you can write code like the following:

```
~~~cpp
vector<string>::value_type s1 = input[0];  // s1 is type string
vector<string>::reference s2 = input[1];   // s2 is type string &
~~~
```

This results in `s1` being a new `string` object that's a copy of `input[0]` and in `s2` being a reference to `input[1]`. In this example, given that you already know that the template is based on the `string` type, it would be simpler to write the following code, which is equivalent in its effect:

```
~~~cpp
string s1 = input[0];      // s1 is type string
string & s2 = input[1];    // s2 is type string &
~~~
```

However, the more elaborate types from Table G.1 can also be used in more general code in which the type of container and element are generic. For example, suppose you want a `min()` function that takes as its argument a reference to a container and returns the smallest item in the container. This assumes that the `<` operator is defined for the value type used to instantiate the template and that you don't want to use the STL `min_element()` algorithm, which uses an iterator interface. Because the argument could be `vector<int>` or `list<string>` or `deque<double>`, you use a template with a template parameter, such as `Bag`, to represent the container. (That is, `Bag` is a template type that might be instantiated as `vector<int>`, `list<string>`, or some other container type.) So the argument type for the function is `const Bag & b`. What about the return type? It should be the value type for the container—that is, `Bag::value_type`. However, at this point, `Bag` is just a template parameter, and the compiler has no way of knowing that the `value_type` member is actually a type. But you can use the `typename` keyword to clarify that a class member is a typedef:

```
~~~cpp
vector<string>::value_type st;   // vector<string> a defined class
typename Bag::value_type m;      // Bag an as yet undefined type
~~~
```

For the first definition here, the compiler has access to the `vector` template definition, which states that `value_type` is a typedef. For the second definition, the `typename` keyword promises that, whatever `Bag` may turn out to be, the combination `Bag::value_type` is the name of a type. These considerations lead to the following definition:

```
~~~cpp
template<typename Bag>
typename Bag::value_type min(const Bag & b)
{
    typename Bag::const_iterator it;
    typename Bag::value_type m = *b.begin();
~~~
```