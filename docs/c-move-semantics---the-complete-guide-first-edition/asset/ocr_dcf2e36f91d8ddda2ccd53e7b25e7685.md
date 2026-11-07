# ### 10.2.3 Rvalue References of Parameters in Full Specializations

An rvalue reference to a parameter of a full specialization of a function template is *not* a universal reference. For example:

```
~~~cpp
template<typename T>            // primary template
void foo(T&& arg);              // - arg is a universal reference
...
template<>                      // full specialization (for rvalues only)
void foo(std::string&& arg);    // - arg is not a universal reference
~~~
```

For lvalues of type std::string still the primary template will be called. To specialize all cases of the primary template for std::strings you have to provide a second full specialization:

```
~~~cpp
template<>                      // full specialization (for lvalues)
void foo(std::string& arg);
~~~
```

Here is a complete example:

*generic/universalspec.cpp*

```
~~~cpp
#include <iostream>
#include <string>
#include <vector>

// primary template taking a universal reference:
template<typename Coll, typename T>
void insert(Coll& coll, T&& arg)
{
    std::cout << "primary template for type T called\n";
    coll.push_back(arg);
}

// full specialization for rvalues of type std::string:
template<>
void insert(std::vector<std::string>& coll, std::string&& arg)
{
    std::cout << "full specialization for type std::string&& called\n";
    coll.push_back(arg);
}

// full specialization for lvalues of type std::string:
template<>
void insert(std::vector<std::string>& coll, const std::string& arg)
{
    std::cout << "full specialization for type const std::string& called\n";
    coll.push_back(arg);
}
~~~
```