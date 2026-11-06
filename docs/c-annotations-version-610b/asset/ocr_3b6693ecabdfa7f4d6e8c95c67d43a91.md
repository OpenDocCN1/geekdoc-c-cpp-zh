```
```cpp
{
    return lvalue + mvalue + rvalue;
}
```
```

The overloaded function does not have to be defined in terms of simple values. Like all overloaded functions, a unique set of function parameters is enough to define an overloaded function template. For example, here's an overloaded version that can be used to compute the sum of the elements of a vector:

```
```cpp
template <typename Type>
Type add(std::vector<Type> const &vect)
{
    return accumulate(vect.begin(), vect.end(), Type());
}
```
```

When overloading function templates we do not have to restrict ourselves to the function's parameter list. The template's type parameter list itself may also be overloaded. The last definition of the `add` template allows us to specify a `vector` as its first argument, but no `deque` or `map`. Overloaded versions for those types of containers could of course be constructed, but how far should we go? A better approach seems to be to look for common characteristics of these containers. If found we may be able to define an overloaded function template based on these common characteristics. One common characteristic of the mentioned containers is that they all support `begin` and `end` members, returning iterators. Using this, we could define a template type parameter representing containers that must support these members. But mentioning a plain `container type` doesn't tell us for what type of data it was instantiated. So we need a second template type parameter representing the container's data type, thus overloading the template's type parameter list. Here is the resulting overloaded version of the `add` template:

```
```cpp
template <typename Container, typename Type>
Type add(Container const &cont, Type const &init)
{
    return std::accumulate(cont.begin(), cont.end(), init);
}
```
```

One may wonder whether the `init` parameter could not be left out of the parameter list as `init` often has a default initialization value. The answer is 'yes', but there are complications. It is possible to define the `add` function as follows:

```
```cpp
template <typename Type, typename Container>
Type add(Container const &cont)
{
    return std::accumulate(cont.begin(), cont.end(), Type());
}
```
```

Note, however, that the template's type parameters were reordered, which is necessary because the compiler won't be able to determine `Type` in a call like:

```
```cpp
int x = add(vectorOfInts);
```
```

After reordering the template type parameters, putting `Type` first, an explicit template type argument can be provided for the first template type parameter:

```
```cpp
int x = add<int>(vectorOfInts);
```
```

In this example we provided a `vector<int>` argument. One might wonder why we have to specify `int` explicitly to allow the compiler to determine the template type parameter `Type`. In fact, we don't. A third kind of template parameter exists, a *template template parameter*, allowing the compiler to determine `Type` directly from the actual container argument. Template template parameters are discussed in section 22.4.