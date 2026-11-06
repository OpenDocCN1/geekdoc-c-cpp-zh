```
```cpp
template <typename Type>
Type function(Type t)
{
    Type::Ambiguous *ptr;

    return t + *ptr;
}
```
```

When this code is processed by the compiler, it complains with an -at first sight puzzling- error message like:

```
```text
4: error: ’ptr’ was not declared in this scope
```
```

The error message is puzzling as it was the programmer’s intention to declare a pointer to a type `Ambiguous` defined within the class template `Type`. But the compiler, confronted with `Type::Ambiguous` may interpret the statement in various ways. Clearly it cannot inspect `Type` itself trying to uncover `Type`’s true nature as `Type` is a template type. Because of this `Type`’s actual definition isn’t available yet.

The compiler is confronted with two possibilities: either `Type::Ambiguous` is a *static member* of the `as yet mysterious` template `Type`, or it is a *subtype* of `Type`. As the standard specifies that the compiler must assume the former, the statement

```
```cpp
Type::Ambiguous *ptr;
```
```

is interpreted as a *multiplication* of the static member `Type::Ambiguous` and the (now undeclared) entity `ptr`. The reason for the error message should now be clear: in this context `ptr` is unknown.

To disambiguate code in which an identifier refers to a subtype of a template type parameter the keyword `typename` must be used. Accordingly, the above code is altered into:

```
```cpp
template <typename Type>
Type function(Type t)
{
    typename Type::Ambiguous *ptr;

    return t + *ptr;
}
```
```

Classes fairly often define subtypes. When such subtypes appear inside template definitions as subtypes of template type parameters the typename keyword must be used to identify them as subtypes. Example: a class template `Handler` defines a typename `Container` as its template type parameter. It also defines a data member storing the iterator returned by the container’s begin member. In addition Handler offers a constructor accepting any container supporting a `begin` member. Handler’s class interface could then look like this:

```
```cpp
template <typename Container>
class Handler
{
    Container::const_iterator d_it;

public:
    Handler(Container const &container)
    :
        d_it(container.begin())
    {}
};
```
```