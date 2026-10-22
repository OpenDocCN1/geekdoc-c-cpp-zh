# 11.5 Defer Evaluations

When implementing templates, sometimes the question comes up whether the code can deal with incomplete types (see Section 10.3.1 on page 154). Consider the following class template: Click here to view code image

```
template<typename T>
class Cont {
private:
T* elems;
public:
... 
};
```

So far, this class can be used with incomplete types. This is useful, for example, with classes that refer to elements of their own type: Click here to view code image

```
struct Node
{
std::string value;
Cont<Node> next; // only possible if Cont accepts incomplete types
};
```

However, for example, just by using some traits, you might lose the ability to deal with incomplete types. For example: Click here to view code image

```
template<typename T>
class Cont {
private:
T* elems;
public:
...
typename std::conditional<std::is_move_constructible<T>::value,
T&&,
T&
>::type
foo();
};
```

Here, we use the trait std::conditional (see Section D.5 on page 732) to decide whether the return type of the member function foo() is T&& or T&. The decision depends on whether the template parameter type T supports move semantics.

The problem is that the trait std::is_move_constructible requires that its argument is a complete type (and is not void or an array of unknown bound; see Section D.3.2 on page 721). Thus, with this declaration of foo(),