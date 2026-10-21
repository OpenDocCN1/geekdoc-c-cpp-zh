```
ps[0] = "hello";    // ERROR

std::shared_ptr<std::string[]> parr{new std::string[10]};
*parr = "hello";    // ERROR (unspecified behavior)
parr[0] = "hello";  // OK
```

Note that there is no formal specification of whether operator* is supported for allocated raw arrays and whether operator[] is supported otherwise. However, usually calling these unspecified operations does not compile.

# 28.2.2 reinterpret_pointer_cast for Shared Pointers

In addition to static_pointer_cast, dynamic_pointer_cast, and const_pointer_cast, you can now call reinterpret_pointer_cast to reinterpret the type of the bits a shared pointer refers to.

# 28.2.3 weak_type for Shared Pointers

To support the use of weak pointers in generic code, shared pointers now provide a member weak_type.
For example:

```
template<typename T>
void observe(T sp)
{
    // initialize weak pointer from passed shared pointer:
    typename T::weak_type wp{sp};
    ...
}
```

# 28.2.4 weak_from_this for Shared Pointers

Sometimes you need another shared pointer to an existing object without having access to the existing shared pointer(s). For this problem, C++11 introduced the base class enable_shared_from_this, which provides the member function shared_from_this:

```
#include <memory>

class Person : public std::enable_shared_from_this<Person>
{
    ...
};

Person* pp = new Person{...};
std::shared_ptr<Person> sp1{pp};  // sp1 gets owner
std::shared_ptr<Person> sp2{pp};  // fatal runtime ERROR: sp2 gets independent owners
std::shared_ptr<Person> sp3{pp->shared_from_this()}; // OK: sp1 and sp3 share ownership
```