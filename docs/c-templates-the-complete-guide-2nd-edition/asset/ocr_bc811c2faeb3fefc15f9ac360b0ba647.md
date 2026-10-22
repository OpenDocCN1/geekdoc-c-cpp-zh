```
{
assert(!elems.empty());
elems.pop_back(); // remove last element
}
```

```
template<typename T>
T const& Stack<T>::top () const
{
assert(!elems.empty());
return elems.back(); // return copy of last element
}
```

As you can see, the class template is implemented by using a class template of the C++ standard library: vector<>. As a result, we don’t have to implement memory management, copy constructor, and assignment operator, so we can concentrate on the interface of this class template.

# 2.1.1 Declaration of Class Templates

Declaring class templates is similar to declaring function templates: Before the declaration, you have to declare one or multiple identifiers as a type parameter(s). Again, T is usually used as an identifier: Click here to view code image

```
template<typename T>
class Stack {
...;
};
```

Here again, the keyword class can be used instead of typename: Click here to view code image

```
template<class T>
class Stack {
...;
};
```

Inside the class template, T can be used just like any other type to declare members and member functions. In this example, T is used to declare the type of the elements as vector of Ts, to declare push() as a member function that uses a T as an argument, and to declare top() as a function that returns a T: Click here to view code image

```
template<
typename T>
class Stack {
```