
In a similar way, we can constrain generic code to let universal references bind to rvalues only. However, none of this would be necessary if we had a specific syntax for universal references. For example:

```cpp
void processString(std::string&&& arg);  // assume &&& declares a universal reference
```

We do not have this specific syntax, however, and now we have existing code with both applications of &&.

## 10.2 Universal or Ordinary Rvalue Reference?

The fact that we use the same syntax for ordinary rvalue references and universal/forwarding references introduces some interesting corner cases for the question of whether an object is an ordinary rvalue reference or a universal reference.

### 10.2.1 Rvalue References of Members of Generic Types

An rvalue reference to a member type of a template parameter is *not* a universal reference. For example:

```cpp
template<typename T>
void foo(typename T::value_type&& arg);  // not a universal reference
```

Here is a complete example:

*generic/universalmem.cpp*

```cpp
#include <iostream>
#include <string>
#include <vector>

template<typename T>
void insert(T& coll, typename T::value_type&& arg)
{
    coll.push_back(arg);
}

int main()
{
    std::vector<std::string> coll;
    …
    insert(coll, std::string{"prvalue"});  // OK
    …
    std::string str{"lvalue"};
    insert(coll, str);             // ERROR: T::value_type&& is not a universal reference
    insert(coll, std::move(str));  // OK
    …
}
```

### 10.2.2 Rvalue References of Parameters in Class Templates

An rvalue reference to a template parameter of a class template is *not* a universal reference.

For example:

```cpp
template<typename T>
class C {
    T&& member;          // member is not a universal reference
    ...
    void foo(T&& arg);   // arg is not a universal reference
};
```

Here is a complete example:

*generic/universalclass.cpp*

```cpp
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
    values.push_back(val);
  }
};

int main()
{
  Coll<std::string> coll;
  ...
  coll.insert(std::string{"prvalue"});  // OK
  std::string str{"lvalue"};
  coll.insert(str);              // ERROR: T&& of Coll<T> is not a universal reference
  coll.insert(std::move(str));   // OK
  ...
}
```

In general, a function in a class template does not follow the rule of function templates. It is what we call a *temploid*, generic code that follows the rules of ordinary functions when we instantiate the class.

### 10.2.3 Rvalue References of Parameters in Full Specializations

An rvalue reference to a parameter of a full specialization of a function template is *not* a universal reference. For example:

```cpp
template<typename T>            // primary template
void foo(T&& arg);              // - arg is a universal reference
...
template<>                      // full specialization (for rvalues only)
void foo(std::string&& arg);    // - arg is not a universal reference
```

For lvalues of type std::string still the primary template will be called. To specialize all cases of the primary template for std::strings you have to provide a second full specialization:

```cpp
template<>                      // full specialization (for lvalues)
void foo(std::string& arg);
```

Here is a complete example:

*generic/universalspec.cpp*

```cpp
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

int main()
{
    std::vector<std::string> coll;
    ...
    insert(coll, std::string{"prvalue"});   // calls full specialization for rvalues
    std::string str{"lvalue"};
    insert(coll, str);                       // calls full specialization for lvalues
    insert(coll, std::move(str));            // calls full specialization for rvalues
    ...
}
```

Note that you have to declare/define full specializations of member function templates outside the class definition:

```cpp
template<typename T>
class Cont {
    ...
    // primary template:
    template<typename U>
    void insert(U&& v) {    // universal reference
        coll.push_back(std::forward<U>(v));
    }
};
...

// full specializations for Cont<T>::insert<>():
// - have to be outside the class
// - need specializations for rvalues and lvalues

template<>
    template<>
void Cont<std::string>::insert<>(std::string&& v)
{
    coll.push_back(std::move(v));
}

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

```cpp
template<typename T>
void f(T&& arg)              // arg is universal forwarding reference
{
    g(std::forward<T>(arg));  // perfectly forward (move() only for passed rvalues)
}
```

Normally, T would just have the type of the passed argument:

```cpp
MyType v;

f(MyType{});                // T is deduced as MyType, so arg is declared as MyType&&
f(std::move(v));            // T is deduced as MyType, so arg is declared as MyType&&
```

However, for universal references, there is a special rule, if lvalues are passed (see the section [temp.deduct.call] of the C++ standard):

If the parameter type is an rvalue reference to a cv-unqualified template parameter and the argument is an lvalue, the type “lvalue reference to T” is used in place of T for type deduction.

That means that in this case:

- If the type of the parameter arg is declared with && and not declared with const or volatile
- and an lvalue is passed
- then T is deduced as T& instead.

In our example, that means:

```cpp
template<typename T>
void f(T&& arg);             // arg is a universal forwarding reference

MyType v;
const MyType c;

f(v);                       // T is deduced as MyType&
f(c);                       // T is deduced as const MyType&
```

However, we have arg declared as T&&. So, if T is T& instead, what does that mean? Here, the *reference collapsing* rule of C++ (see the section [dcl.ref] of the C++ standard) gives an answer:

- `T& &` becomes `T&`
- `T& &&` becomes `T&`
- `T&& &` becomes `T&&`
- `T&& &&` becomes `T&&`

1. Since C++17, the C++ standard uses the term *forwarding reference* in this definition.

That means:

```cpp
MyType v;
const MyType c;

f(v);    // T is deduced as MyType& and arg has this type
f(c);    // T is deduced as const MyType& and arg has this type
```

Now consider how std::forward<> is defined in contrast to std::move():

- `std::move()` always converts any type to an rvalue reference:

  `static_cast<remove_reference_t<T>&&>(t)`

  It removes any references and converts to the corresponding rvalue reference type (removes any & and adds &&).

- `std::forward<>` only adds rvalue referenceness to the passed type parameter:

  `static_cast<T&&>(t)`

Here, the reference collapsing rules apply again:

- If type T is an lvalue reference, T&& is still an lvalue reference (&& has no effect). Therefore, we cast arg to an lvalue reference, which means that arg has no move semantics.
- However, if T is an rvalue reference (or not a reference at all), T&& is (still) an rvalue reference. Therefore, we cast arg to an rvalue reference and that way we change the value category to an xvalue, which is the effect of std::move().

In total, therefore, we get:

```cpp
template<typename T>
void f(T&& arg)              // arg is a universal/forwarding reference
{
    g(std::forward<T>(arg));  // perfectly forward (move() only for passed rvalues)
}
```

```cpp
MyType v;
const MyType c;

f(v);             // T and arg are MyType&, forward() has no effect in this case
f(c);             // T and arg are const MyType&, forward() has no effect in this case
f(MyType{});      // T is MyType, arg is MyType&&, forward() is equivalent to move()
f(std::move(v));  // T is MyType, arg is MyType&&, forward() is equivalent to move()
```

Note that string literals are lvalues so that we deduce T and arg for them as follows:

```cpp
f("hi");              // lvalue passed, so T and arg have type const char (&)[3]
f(std::move("hi"));   // rvalue passed, so T is deduced as const char [3]
                       //              and arg has type const char (&&)[3]
```
