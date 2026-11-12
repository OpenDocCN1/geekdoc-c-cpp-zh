```
```text
virtual_template.cpp:5:5: error:
'virtual' can not be specified on member
    function templates
    virtual void f(U);
    ~~~~~~~
1 error generated.
```
```

A member function template can not be virtual.

# *** Question 212　 override virtual and template

Which of the following member function overrides B::f(int)?

```
```cpp
class B
{
    virtual void f(int);
};
class D : public B
{
    template <class T>
    void f(T);
    void f(int i)
    {
        f<>(i);
    }
};
```
```

# Solution of Question 212

A specialization of a member function template does not override a virtual function from a base class. Hence `template <class T> void f(T)` does not override `B::f(int)`. `void f(int i)` is the overriding function that calls the template instantiation.

# *** Question 213　 parameter pack

What is a template parameter pack and function parameter pack?

# Solution of Question 213

A template parameter pack is a template parameter that accepts zero or more template arguments. For example:

```
```cpp
template<class ... Types> struct Tuple { };
Tuple<> t0;                  // Types contains no arguments
Tuple<int> t1;               // Types contains one argument : int
Tuple<int, float> t2;        // Types contains two arguments : int and float
Tuple<> error;               // error : <> is not a type
```
```