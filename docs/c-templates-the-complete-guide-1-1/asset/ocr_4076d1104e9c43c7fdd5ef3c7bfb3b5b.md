```
```cpp
assert (alice.empty());

alice.push_back(1); // reserve copy of last
}
```
```

As you can see, the class template is implemented by using a class template of the C++ standard library `vector<>`. As a result, we don't have to implement memory management, copy constructor, and assignment operator, so on account of no interface of this class template.

# ### 2.1.1 Declaration of Class Templates

Declaring a class template is similar to declaring function templates: Before the declaration, you have to declare the identifier or multiple identifiers as a type parameter(s). Again, a type is usually used as an identifier.

[Click here to view code image](#)

```
```cpp
template<typename T>
class Stack {
...
};
```
```

Here again, the keyword class can be used instead of typename:

[Click here to view code image](#)

```
```cpp
template<class T>
class Stack {
...
};
```
```

Inside the class template, T can be used just like any other type to declare members and member functions. In this example, T is used to declare the member function that uses a T as an argument, and to declare a push() as a function that returns T:

[Click here to view code image](#)

```
```cpp
template<typename T>
class Stack {
private:
    std::vector<T> elems; // elements
public:
    void push(T const& elem); // push element
    void pop(); // pop element
    T top() const; // return top element
    bool empty() const { // return whether the
        return elems.empty();
    }
};
```
```

The type of this class is `Stack<T>`, with T being a template parameter. Thus, you have to use `Stack<>` whenever you use one of this class in a declaration except in cases where the template arguments can be deduced from the arguments of a member function. However, inside the class template you have to deal with the template arguments in accordance with the type of template parameters, as its argument (see Section 2.1.3 on page 221 for details).

For example, if you have to define your own copy constructor and assignment operator, typically looks like this:

[Click here to view code image](#)

```
```cpp
template<typename T>
class Stack {
    Stack (Stack const&); // copy constructor
    Stack& operator= (Stack const&); // assignment operator
};
```
```

which is formally equivalent to:

[Click here to view code image](#)

```
```cpp
template<typename T>
class Stack {
    Stack (Stack<T> const&); // copy constructor
    Stack<T>& operator= (Stack<T> const&); // assignment operator
};
```
```

but usually the `<T>` engenders special handling of special template parameters, so it's usually better to use the first form.

However, inside the class structure you'd need:

[Click here to view code image](#)

```
```cpp
template<typename T>
bool operator== (Stack<T> const &, Stack<T> const&);
```
```

Note that in places where the name and not the type of the class is required, only Stack may be used. This is especially the case when you use the name of the class in a class declaration, or in a member function.