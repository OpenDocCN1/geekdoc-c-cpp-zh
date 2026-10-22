

`is_move_assignable_v<int>`          // 结果为 true
`is_move_assignable_v<int&>`         // 结果为 true
`is_move_assignable_v<int&&>`        // 结果为 true
`is_move_assignable_v<void>`         // 结果为 false
`is_move_assignable_v<void*>`        // 结果为 true
`is_move_assignable_v<char[]>`       // 结果为 false
`is_move_assignable_v<std::string>`  // 结果为 true
`is_move_assignable_v<std::unique_ptr<int>>`  // 结果为 true

`is_destructible_v<void>`                  // 结果为 false
`is_destructible_v<int>`                   // 结果为 true
`is_destructible_v<std::string>`           // 结果为 true
`is_destructible_v<std::pair<int,std::string>>` // 结果为 true

`is_trivially_destructible_v<void>`        // 结果为 false
`is_trivially_destructible_v<int>`         // 结果为 true
`is_trivially_destructible_v<std::string>` // 结果为 false
`is_trivially_destructible_v<std::pair<int,int>>` // 结果为 true
`is_trivially_destructible_v<std::pair<int,std::string>>` // 结果为 false

`is_swappable_v<int>`                     // 结果为 true
`is_swappable_v<int&>`                    // 结果为 true
`is_swappable_v<int&&>`                   // 结果为 true
`is_swappable_v<std::string&&>`           // 结果为 true
`is_swappable_v<void>`                    // 结果为 false
`is_swappable_v<void*>`                   // 结果为 true
`is_swappable_v<char[]>`                  // 结果为 false
`is_swappable_v<std::unique_ptr<int>>`    // 结果为 true

```cpp
auto a = nullptr;
auto b = nullptr;
is_same_v<decltype(a),decltype(b)>      // 结果为 true
```

```cpp
using A = int;
is_same_v<A,int>                        // 结果为 true
```

```cpp
auto x = [] (int) {};
auto y = x;
auto z = [] (int) {};
is_same_v<decltype(x),decltype(y)>      // 结果为 true
is_same_v<decltype(x),decltype(z)>      // 结果为 false
```

```cpp
class B {
};
class D1 : B {
};
class D2 : B {
};
class DD : private D1, private D2 {
};
is_base_of_v<B, D1>      // 结果为 true
is_base_of_v<B, DD>      // 结果为 true
is_base_of_v<B const, DD> // 结果为 true
is_base_of_v<B, DD const> // 结果为 true
is_base_of_v<B, B const> // 结果为 true
is_base_of_v<B&, DD&>    // 结果为 false（非类类型）
is_base_of_v<B[3], DD[3]> // 结果为 false（非类类型）
is_base_of_v<int, int>   // 结果为 false（非类类型）
```

```cpp
auto test() {
    return std::declval<FROM>();
}

class C {
    public:
        explicit C(C const&);  // 没有隐式复制构造函数
        ...
};

is_constructible_v<C,C>      // 结果为 true
is_convertible_v<C,C>        // 结果为 false
```

```cpp
remove_cv_t<int>                       // 结果为 int
remove_const_t<int const>              // 结果为 int
remove_cv_t<int const volatile>         // 结果为 int
remove_const_t<int const&>              // 结果为 int const&（仅移除const限定符，不作用于引用）
```

```cpp
remove_const_t<remove_reference_t<int const&>>  // 结果为 int
remove_reference_t<remove_const_t<int const&>>  // 结果为 int const
```

```cpp
decay_t<int const&>    // 结果为 int
```

```cpp
add_cv_t<int>                  // 结果为 int const volatile
add_cv_t<int const>             // 结果为 int const volatile
add_cv_t<int const volatile>    // 结果为 int const volatile
add_const_t<int>                // 结果为 int const
add_const_t<int const>           // 结果为 int const
add_const_t<int&>                // 结果为 int&
```

```cpp
make_unsigned_t<char>      // 结果为 unsigned char
make_unsigned_t<int>       // 结果为 unsigned int
make_unsigned_t<int const&> // 未定义行为
```

```cpp
remove_const_t<remove_reference_t<int const&>> // 结果为 int
remove_reference_t<remove_const_t<int const&>> // 结果为 int const
```

```cpp
decay_t<int const&> // 结果为 int
```

```cpp
remove_pointer_t<int>              // 结果为 int
remove_pointer_t<int const*>       // 结果为 int const
remove_pointer_t<int const* const* const> // 结果为 int const* const
```

```cpp
add_pointer_t<void>          // 结果为 void*
add_pointer_t<int const* const>  // 结果为 int const* const*
add_pointer_t<int&>            // 结果为 int*
add_pointer_t<int [3]>         // 结果为 int(*) [3]
add_pointer_t<void(&)(int)>    // 结果为 void(*)(int)
add_pointer_t<void(int)>       // 结果为 void(*)(int)
add_pointer_t<void(int) const> // 结果为 void(int) const（无变化）
```

```cpp
remove_extent_t<int>                // 结果为 int
remove_extent_t<int[10]>            // 结果为 int
remove_extent_t<int[5][10]>         // 结果为 int[10]
remove_extent_t<int[][10]>          // 结果为 int[10]
remove_extent_t<int*>               // 结果为 int*
remove_all_extents_t<int>           // 结果为 int
remove_all_extents_t<int[10]>       // 结果为 int
remove_all_extents_t<int[5][10]>    // 结果为 int
remove_all_extents_t<int[][10]>     // 结果为 int
remove_all_extents_t<int(*) [5]>    // 结果为 int(*) [5]
```

```cpp
decay_t<int const&>      // 结果为 int
decay_t<int const[4]>   // 结果为 int const*
void foo();
decay_t<decltype(foo)>  // 结果为 void(*)()
```

```cpp
using POD_T = std::aligned_union_t<0, char,
    std::pair<std::string,std::string>>;
std::cout << sizeof(POD_T) << '\n';
std::cout << std::aligned_union<0, char,
    std::pair<std::string,std::string>
>::alignment_value;
    << '\n';
```

```cpp
using POD_T = std::aligned_storage_t<5>;

struct X {
    X(int);    // 从int转换而来
};
struct Y;    // 不完整类型

// 未定义行为：
static_assert(std::is_constructible<X,int>{}
    || std::is_constructible<Y,int>{},
    "can't init X or Y from int");

// 正确写法：
static_assert(std::disjunction<std::is_constructible<X, int>,
    std::is_constructible<Y, int>>{},
    "can't init X or Y from int");

template<typename T>
struct isNoPtrT : std::negation<std::disjunction<std::is_null_pointer<T>,
    std::is_member_pointer<T>,
    std::is_pointer<T>>>
{
};
```

```cpp
std::cout << isNoPtrT<void*>::value << '\n';        //false
std::cout << isNoPtrT<std::string>::value << '\n';  // true
auto np = nullptr;
std::cout << isNoPtrT<decltype(np)>::value << '\n';  //false
```

```cpp
template<typename T>
constexpr bool isNoPtr = isNoPtrT<T>::value;
```

```cpp
std::cout << isNoPtr<void*> << '\n';    // false
std::cout << isNoPtr<int> << '\n';    // true
```

```cpp
template<typename... Ts>
std::enable_if_t<std::conjunction_v<std::negation<std::is_class<Ts>>...,
    std::negation<std::is_union<Ts>>...
    >>
print(Ts...)
{
    ...
}
```

