5. move assignment operator

```
~~~cpp
A& operator=(A&& a)
{
    _str =
        static_cast<std::string&&>(a._str);
    return *this;
}
~~~
```

or,

```
~~~cpp
A& operator=(A&& a)
{
    _str = std::move(a._str);
    return *this;
}
~~~
```

6. destructor

```
~~~cpp
~A() { }
~~~
```

Hence it may look like :

# Program 8.12: Compiler Generated Member Functions

```
~~~cpp
#include <string>
struct A
{
    std::string _str;

    A() : _str() { }

    A(const A & a): _str(a._str) { }

    A(A&& a)
    :
        _str(static_cast<std::string&&>(a._str)) { }

    A& operator=(const A& a)
    {
        _str = a._str;
    }
~~~
```