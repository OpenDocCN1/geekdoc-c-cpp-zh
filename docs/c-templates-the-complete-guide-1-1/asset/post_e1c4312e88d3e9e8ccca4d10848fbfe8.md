
```cpp
#include "SpaceClassInscript3.hpp"

int main()
{
    ...

    std::string s = "...";

    Person p1(s);                 // init with string object
    Person p2("...");             // init with string literal
    Person p3(p1);                // OK -- calls COPY-CON...
    Person p4(std::move(p1));      // OK -- calls MOVE-CON...
}
```

Note again that in C++14, we have to declare the alias template as follows, because the `_t` version is not defined for type traits that yield a value:

**Click here to view code image**

```cpp
template<typename T>
using EnableIfString = std::enable_if_t<
    std::is_convertible<T, std::string>::value,
    std::string>;
```

And in C++11, we have to declare the special member template as follows, because as written the `_t` version is not defined for type traits that yield a value:

**Click here to view code image**

```cpp
template<typename T>
using EnableIfString =
    typename std::enable_if<
        std::is_convertible<T, std::string>::value
    >::type;
```

But that's still not quite the definition of `enable_if<>`:

Note also that there is an alternative to `std::is_convertible<>` because it requires that the types are implicitly convertible. By using `std::is_constructible<>`, we also allow explicit conversions to be used for the initialization. However, the order of the arguments is the opposite in this case.

**Click here to view code image**

```cpp
template<typename T>
using EnableIfString =
    std::enable_if_t<
        std::is_constructible<T, std::string>::value,
        std::string>;
```

See Section 3.3.2 on page 730 for details about `std::is_constructible<>` and Section 3.3.3 on page 727 for details and examples to apply `enable_if<>` on various template patterns.

### Disabling Special Member Functions

Note that normally we can't use `enable_if<>` to disable the predefined copy/move constructors and/or assignment operators. The reason is that member function templates never count as special member functions and are ignored when, for example, a copy constructor is needed. Thus, with this declaration:

**Click here to view code image**

```cpp
class C
{
public:
    template<typename T>
    C(T const&)
    {
        // ...
    }
};
```

the predefined copy constructor is still used, when a copy of a `C` is requested:

**Click here to view code image**

```cpp
C x;
C y(x);  // still uses the predefined copy constructor
         // (not the member template)
```

There is really no way to use the member template because there is no way to specify or deduce its template parameter `T`.

Deleting the predefined copy constructor is no solution, because then the trial to copy a `C` results in an error.

There is a tricky solution, though: We can declare a copy constructor for `const volatile` arguments and mark it "deleted" (i.e., define it with `= delete`). Doing so prevents another copy constructor from being implicitly deleted. With this in place, we can define a constructor template that will be preferred over the (deleted) copy constructor for nonvolatile types:

```cpp
// user-define the predefined copy constructor as
// deleted
// (with conversion to volatile to enable better
// matching)
C(const volatile&) = delete;

// implement copy constructor template with better
// match
template<typename U>
C(C<U> const&) {
    // ...
}
```

Now the template constructors are used even for "normal" copying.

**Click here to view code image**

```cpp
C x;
C y(x); // uses the member template
```

In such a template constructor we can then apply additional constraints with `enable_if`. For example, to prevent being able to copy objects of a class template `C` from the template parameter in a template type, we can implement the following:

**Click here to view code image**

```cpp
template<typename T>
class C
{
public:
    // ... define the predefined copy constructor as
    // deleted
    // (with conversion to volatile to enable better
    // matching)
    C(const volatile&) = delete;

    // If T is not integral type, provide copy constructor
    template<typename U,
             typename = std::enable_if_t<std::is_integral_v<U>>>
    C(C<U> const&) {
    }
};
```

### 6.5 USING CONCEPTS TO SIMPLIFY NEARLY-IF EXPRESSIONS

Even when using aliases/templates, the `enable_if` syntax is pretty clumsy, because it uses a work-around: To get the desired effect, we add an additional template parameter and “abuse” that parameter to provide a specific requirement for the function template to be available at all. Code like this is hard to read and makes the rest of the function template hard to understand.

In principle, we just need a language feature that allows us to formulate requirements or constraints for a function in a way that causes that function to be ignored if the requirements/constraints are not met.

This is an application of the long-awaited language feature concepts, which allows us to formulate requirements/conditions for templates with its own simple syntax. Unfortunately, although long discussed, concepts still did not become part of the C++17 standard. Some companies provide experimental support for such a feature, however, and concepts will likely become part of the next standard after C++17.

With concepts, as their use is proposed, we simply have to write the following:

**Click here to view code image**

```cpp
template<typename T>
requires std::is_convertible_v<T, std::string>
Person(const T& name) : name(std::forward<T>(name)) {
}
```

### 6.6 SUMMARY

In templates, we can “perfectly” forward parameters by declaring them as forwarding references (declared with a type format with the name of a template parameter followed by &&) and using std::forward<> in the forwarded call.

- When using perfect forwarding member function templates, they might match better than the predefined special member function to copy or move objects.

- With std::enable_if_t<…>, you can disable a function template when a wrong-type condition is false (the template is then ignored when that condition has been determined).

- By using std::enable_if_t<> you can avoid problems when constructor templates or assignment operator templates that can be called for single arguments are a better match than implicitly generated special member functions.

- You can simplify (and apply enable_if_t<> to) special member functions by deleting the predefined special member functions for const-volatile objects.

- Concepts allow you to use a more intuitive syntax for requirements on function templates.

¹ The fact that move semantics is not automatically passed through is intentional and important. If it weren’t, we would have the value of a moved-from object the first time we use it in a function.

² A type like X const& is valid but provides no common semantics in practice because “stealing” the internal representation of a movable object requires modifying that object. It might be used, though, to force passing other temporaries or objects marked with std::move() without being able to modify them.

³ The term universal reference was coined by Scott Meyers as a common term that could result in either an “rvalue reference” or an “lvalue reference.” Because “universal” was, well, too universal, the C++ standard introduced the term forwarding reference, because the major reason to use such a reference is to forward objects. However, note that it does not automatically forward. The term does not describe what it is but what it is typically used for.

⁴ Don’t forget to place the condition into parentheses, because otherwise the > in the condition would end the template argument list.

⁵ Thanks to Stephen C. Dewhurst for pointing that out.

⁶ If you wonder why we don’t instead check whether std::is_not_convertible, because we are defining a function that might allow us to convert a string to a person. So the constructor has to know whether it is enabled, which depends on whether it is enabled, and so on. Never use enable_if_t in a place that impacts the condition used by enable_if. This is a logical error that compilers do not necessarily detect.

⁷ Thanks to Peter Dimov for pointing out this technique.
