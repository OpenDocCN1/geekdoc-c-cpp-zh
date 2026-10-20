
## 10.2 Universal or Ordinary Rvalue Reference?

Since C++20, constraining a universal reference to specific types is possible with concepts and the keyword requires. However, you have to decide whether and which kind of type conversions you support:

- When the type must match (no implicit conversions allowed):

```
template<typename T>
requires std::same_as<std::remove_cvref_t<T>, std::string>
void processString(T&&) {
  ...
}
```

- When implicit conversions should be allowed:

```
template<typename T>
requires std::convertible_to<T, std::string>
void processString(T&&) {
  ...
}
```

- When even explicit conversions should be allowed:

```
template<typename T>
requires std::constructible_from<std::string, T>
void processString(T&&) {
  ...
}
```

Usually, std::convertible_to is what you want because it fits with the usual rules of function calls.

Note that std::convertible_to and std::constructible_from have the opposite order for source and destination type of the conversion.

See generic/universaltype.cpp for a complete example with all cases.

Before C++20, you need the enable_if<> type trait instead of requires and the shortcuts with the _v and _t suffixes for type traits might not have been supported. For example, the following code supports all types that are implicitly convertible to std::string since C++11:

```
template<typename T,
typename = typename std::enable_if<
std::is_convertible<T, std::string>::value
>::type>
void processString(T&& args);
```

To restrict to type std::string in C++11, we need:

```
template<typename T,
typename = typename std::enable_if<
std::is_same<typename std::decay<T>::type, std::string>::value
>::type>
void processString(T&& arg);
```

Here, the type trait std::decay<> is used to remove both referenceness and constness from type T (the type trait std::remove_cvref<> is only provided since C++20).

In a similar way, we can constrain generic code to let universal references bind to rvalues only. However, none of this would be necessary if we had a specific syntax for universal references. For example:

```
void processString(std::string&& arg); // assume && declares a universal reference
```

We do not have this specific syntax, however, and now we have existing code with both applications of &&.

The fact that we use the same syntax for ordinary rvalue references and universal/forwarding references introduces some interesting corner cases for the question of whether an object is an ordinary rvalue reference or a universal reference.

An rvalue reference to a member type of a template parameter is not a universal reference.

```
template<typename T>
void foo(typename T::value_type&& arg); // not a universal reference
```

Here is a complete example:

```
#include <iostream>
#include <string>
#include <vector>

template<typename T>
void insert(T coll, typename T::value_type&& arg)
{
	coll.push_back(arg);
}

int main()
{
	std::vector<std::string> coll;
	...
	insert(coll, std::string{"prvalue"}); // OK
	...
	std::string str{"lvalue"};
	insert(coll, str); // ERROR: ::value_type&& is not a universal reference
	insert(coll, std::move(str)); // OK
	...
}
```

### 10.2.2 Rvalue References of Parameters in Class Templates

An rvalue reference to a template parameter of a class template is *not* a universal reference.

For example:

```
template<typename T>
class C {
    T&& member;        // member is not a universal reference
    ...
    void foo(T&& arg);  // arg is not a universal reference
};
```

Here is a complete example:

*generic/universalclass.cpp*

```
#include <iostream>
#include <string>
#include <vector>

template<typename T>
class Coll {
private:
    std::vector<T> values;
public:
    Coll() = default;

    // function in class template:
    void insert(T&& val) {
        values.push_back(std::move(val));
    }
};

int main()
{
    Coll<std::string> coll;
    ...
    coll.insert(std::string{"prvalue"});  // OK
    std::string str{"lvalue"};
    coll.insert(str);                      // ERROR: T&& of Coll<T> is not a universal reference
    coll.insert(std::move(str));           // OK
    ...
}
```

In general, a function in a class template does not follow the rule of function templates. It is what we call a *temploid*, generic code that follows the rules of ordinary functions when we instantiate the class.

### 10.2.3 Rvalue References of Parameters in Full Specializations

An rvalue reference to a parameter of a full specialization of a function template is *not* a universal reference. For example:

```
template<typename T>          // primary template
void foo(T&& arg);           // - arg is a universal reference
...
template<>                   // full specialization (for rvalues only)
void foo(std::string&& arg); // - arg is not a universal reference
```

For lvalues of type std::string still the primary template will be called. To specialize all cases of the primary template for std::strings you have to provide all possible full specializations (including a version for const rvalues):

```
template<>                   // full specialization for const lvalues
void foo(const std::string& arg); // - arg is not a universal reference

template<>                   // full specialization for non-const lvalues
void foo(std::string& arg);    // - arg is not a universal reference

template<>                   // full specialization for non-const rvalues
void foo(std::string&& arg);   // - arg is not a universal reference

template<>                   // full specialization for const rvalues
void foo(const std::string&& arg); // - arg is not a universal reference
```

If you leave out any of the four full specializations, the primary template might be called instead (e.g., if the version for const rvalues is missing, the primary template will be called if you pass a const string marked with std::move()).

Here is a complete example:

*generic/universalspec.cpp*

```
#include <iostream>
#include <string>
#include <vector>

// primary template taking a universal reference:
template<typename Coll, typename T>
void insert(Coll& coll, T&& arg)
{
    std::cout << "primary template for universal reference of type T\n";
    coll.push_back(arg);
}

// full specialization for const lvalues of type std::string:
template<>
void insert(std::vector<std::string>& coll, const std::string& arg)
{
    std::cout << "full specialization for type const std::string&\n";
    coll.push_back(arg);
}

// full specialization for non-const lvalues of type std::string:
template<>
void insert(std::vector<std::string>& coll, std::string& arg)
{
    std::cout << "full specialization for type std::string&\n";
    coll.push_back(arg);
}

// full specialization for non-const rvalues of type std::string:
template<>
void insert(std::vector<std::string>& coll, std::string&& arg)
{
    std::cout << "full specialization for type std::string&&\n";
    coll.push_back(arg);
}

// full specialization for const rvalues of type std::string:
template<>
void insert(std::vector<std::string>& coll, const std::string&& arg)
{
    std::cout << "full specialization for type const std::string&&\n";
    coll.push_back(arg);
}

int main()
{
    std::vector<std::string> coll;
    ...
    insert(coll, std::string{"prvalue"});  // calls full specialization for rvalues
    std::string str{"lvalue"};
    insert(coll, str);                     // calls full specialization for lvalues
    insert(coll, std::move(str));          // calls full specialization for rvalues

    const std::string cstr{"const lvalue"};
    insert(coll, cstr);                    // calls full specialization for const lvalues
    insert(coll, std::move(cstr));         // calls full specialization for const rvalues
}
```

Note that you have to declare/define full specializations of member function templates outside the class definition:

```
template<typename T>
class Cont {
    ...
    // primary template:
    template<typename U>
    void insert(U&& v) {  // universal reference
        coll.push_back(std::forward<U>(v));
    }
    ...
};
```

// full specializations for Cont<T>::insert<>():
// - have to be outside the class
// - need specializations for rvalues and lvalues

```
template<>
template<>
void Cont<std::string>::insert<>(std::string&& v)
{
    coll.push_back(std::move(v));
}
```

```
template<>
template<>
void Cont<std::string>::insert<>(const std::string& v)
{
    coll.push_back(v);
}
```

## 10.3 How the Standard Specifies Perfect Forwarding

To finally understand all rules of perfect forwarding, let us see how the rules are formally specified in the C++ standard.

Again, consider you have the following declaration:

```
template<typename T>
void f(T&& arg)          // arg is universal/forwarding reference
{
    g(std::forward<T>(arg));  // perfectly forward (move() only for passed rvalues)
}
```

Normally, T would just have the type of the passed argument:

```
MyType v;
```
