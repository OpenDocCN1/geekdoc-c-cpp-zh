
## 20.6 Afternotes

The filesystem library was developed under the lead of Beman Dawes for many years as a Boost library. In 2014, for the first time it became a formal beta standard, the *File System Technical Specification* (see http://wg21.link/n4100).

With http://wg21.link/p0218r0 the *File System Technical Specification* was adopted as part of the standard library as proposed by Beman Dawes. Support for computing relative paths was added by Beman Dawes, Nicolai Josuttis, and Jamie Allsop in http://wg21.link/p0219r1. A couple of minor fixes were added as proposed by Beman Dawes in http://wg21.link/p0317r1, by Nicolai Josuttis in http://wg21.link/p0392r0, by Jason Liu and Hubert Tong in http://wg21.link/p0430r2, and especially by the members of the filesystem small group (Beman Dawes, S. Davis Herring, Nicolai Josuttis, Jason Liu, Billy O’Neal, P.J. Plauger, and Jonathan Wakely) in http://wg21.link/p0492r2.

After C++17 was released http://wg21.link/p1164r1 by Nicolai Josuttis fixed the behavior of `make_directory()` as a defect against C++17.

## Part IV

## Library Extensions and Modifications

This part of the book introduces extensions and modifications to existing library components with C++17.

This page is intentionally left blank

## Chapter 21

## Extensions of Type Traits

C++17 extends the general abilities to use type traits (standard type functions) and introduces some new type traits.

### 21.1 Type Traits Suffix _v

Since C++17, you can use the suffix _v for all type traits that yield a value (just like you can use the suffix _t for all type traits that yield a type). For example, for any type T, you can now write:

```
std::is_const_v<T>      // since C++17
```

instead of

```
std::is_const<T>::value  // since C++11
```

This applies to all type traits. The approach is that a corresponding variable template is defined for each standard type trait. For example:

```
namespace std {
    template<typename T>
    constexpr bool is_const_v = is_const<T>::value;
}
```

Such a type trait can be used to formulate Boolean conditions which you can use at runtime:

```
if (std::is_signed_v<char>) {
    ...
}
```

However, because type traits are evaluated at compile time, you can also use the result at compile time (e.g., in a compile-time if statement):

```
if constexpr (std::is_signed_v<char>) {
    ...
}
```

Another application is to support different instantiations of templates:

```
// primary template for class C<T>
template<typename T, bool = std::is_pointer_v<T>>
class C {
    ...
};
```

```
// partial specialization for pointer types:
template<typename T>
class C<T, true> {
    ...
};
```

Here, class C provides a special implementation for pointer types.

The suffix _v can also be used if type traits yield a non-Boolean value, such as std::extent<>, which yields the size of the dimension of a raw array:

```
int a[5][7];
std::cout << std::extent_v<decltype(a)> << '\n';    // prints 5
std::cout << std::extent_v<decltype(a),1> << '\n';  // prints 7
```

### 21.2 New Type Traits

Table New Type Traits lists the new type traits introduced with C++17.

In addition, is_literal_type<> and result_of<> are deprecated since C++17.

The following paragraphs discuss these traits in detail.

#### Type Trait is_aggregate<>

```
std::is_aggregate<T>::value
```

yields whether T is an aggregate type:

```
template<typename T>
struct D : std::string, std::complex<T> {
    std::string data;
};
```

```
D<float> s{"hello", {4.5,6.7}, "world"};        // OK since C++17
std::cout << std::is_aggregate<decltype(s)>::value;  // outputs: 1 (true)
```

| Trait | Effect |
|---|---|
| is_aggregate<T> | Is aggregate type |
| is_swappable<T> | Can call swap() for this type |
| is_nothrow_swappable<T> | Can call swap() for this type and that operation cannot throw |
| is_swappable_with<T,T2> | Can call swap() for these two types with specific value category |
| is_nothrow_swappable_with<T,T2> | Can call swap() for these two types with specific value category and that operation cannot throw |
| has_unique_object_representations<T> | Any two objects with same value have same representation in memory |
| is_invocable<T,Args...> | Can be used as callable for Args... |
| is_nothrow_invocable<T,Args...> | Can be used as callable for Args... without throwing |
| is_invocable_r<RT,T,Args...> | Can be used as callable for Args... returning RT |
| is_nothrow_invocable_r<RT,T,Args...> | Can be used as callable for Args... returning RT without throwing |
| invoke_result<T,Args...> | Result type if used as callable for Args... |
| conjunction<B...> | Logical and for Boolean traits B... |
| disjunction<B...> | Logical or for Boolean traits B... |
| negation<B> | Logical not for Boolean trait B |
| is_execution_policy<T> | Is execution policy type |

Table 21.1. New Type Traits

#### Type Traits is_swappable<> and is_swappable_with<>

```
std::is_swappable<T>::value
std::is_nothrow_swappable<T>::value
std::is_swappable_with<T1,T2>::value
std::is_nothrow_swappable_with<T1,T2>::value
```

yield true if

- Lvalues of type T can be swapped, or
- Values of value category and of type T1 and T2 can be swapped

(with the guarantee that no exception is thrown using the nothrow form).

Note that is_swappable<> and is_nothrow_swappable<> check in general whether you can swap values of a specified type (checking the operation for lvalues). In contrast, is_swappable_with<> and is_nothrow_swappable_with<> take the value category into account. That is,

```
is_swappable_v<int>        // yields true
```

is equivalent to

```
is_swappable_with_v<int&,int&>    // yields true (equivalent)
```

while:
    is_swappable_with_v<int,int>        // yields false
yields false because you cannot call std::swap(42, 77).
For example:

```
is_swappable_v<std::string>        // yields true
is_swappable_v<std::string&>        // yields true
is_swappable_v<std::string&&>       // yields true
is_swappable_v<void>                // yields false
is_swappable_v<void*>               // yields true
is_swappable_v<char[]>              // yields false
```

```
is_swappable_with_v<std::string, std::string>      // yields false
is_swappable_with_v<std::string&, std::string&>    // yields true
is_swappable_with_v<std::string&&, std::string&&> // yields false
```

#### Type Trait has_unique_object_representations<>

```
std::has_unique_object_representations<T>::value
```

yields true if any two objects of type T have the same object representation in memory. That is, two identical values are always represented using the same sequence of byte values.

Objects with this property can produce a reliable hash value by hashing the associated byte sequence (there is no risk that some bits not participating in the object value might differ from one case to another).

#### Type Traits is_invocable<> and is_invocable_r<>

```
std::is_invocable<T,Args...>::value
std::is_nothrow_invocable<T,Args...>::value
std::is_invocable_r<Ret,T,Args...>::value
std::is_nothrow_invocable_r<Ret,T,Args...>::value
```

yield true if you can use T as a callable for Args... returning a value convertible to type Ret (with the guarantee that no exception is thrown). That is, we can use these traits to test whether we can call (directly or via std::invoke()) a callable of type T for arguments of type Args... and use the return value as type Ret.

For example, given:

```
struct C {
    bool operator() (int) const {
        return true;
    }
};
```

we get the following results:

```
std::is_invocable<C>::value        // false
std::is_invocable<C,int>::value    // true
```

```
std::is_invocable<int*>::value                // false
std::is_invocable<int(*)()>::value             // true

std::is_invocable_r<bool,C,int>::value         // true
std::is_invocable_r<int,C,long>::value         // true
std::is_invocable_r<void,C,int>::value         // true
std::is_invocable_r<char*,C,int>::value        // false
std::is_invocable_r<long,int(*)(int)>::value   // false
std::is_invocable_r<long,int(*)(int),int>::value   // true
std::is_invocable_r<long,int(*)(int),double>::value // true
```

#### Type Trait invoke_result<>

```
std::invoke_result<T,Args...>::type
```

yields the return type of using T as the type of a callable for Args.... That is, we can use this trait to get the return type obtained when we call (directly or via std::invoke()) a callable of type T for arguments of type Args....

The trait replaces result_of<>, which should no longer be used.

For example:

```
std::string foo(int);

using T1 = std::invoke_result_t<decltype(foo), int>;    // T1 is std::string

struct ABC {
    virtual ~ABC() = 0;
    void operator() (int) const {
    }
};

using T2 = typename std::invoke_result<ABC, int>::type;  // T2 is void
```

#### Logical Operations for Boolean Type Traits

Table Type Traits to Combine Other Type Traits lists the type traits that are provided to logically combine or apply Boolean type traits (almost all standard type traits that yield a value).

| Traits | Effect |
|---|---|
| conjunction<B...> | Logical and for Boolean traits B... |
| disjunction<B...> | Logical or for Boolean traits B... |
| negation<B> | Logical not for Boolean trait B |

Table 21.2. Type Traits to Combine Other Type Traits
