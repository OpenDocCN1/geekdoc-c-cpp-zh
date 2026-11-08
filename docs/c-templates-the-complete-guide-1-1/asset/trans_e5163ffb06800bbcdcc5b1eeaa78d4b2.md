
```cpp
is_trivially_default_constructible_v<...> // yields false
is_trivially_copyable_v<...>             // yields true
is_trivially_destructible_v<...>         // yields false
is_trivially_copy_constructible_v<...>   // yields true
is_trivially_copy_assignable_v<...>      // yields false
is_trivially_move_constructible_v<...>   // yields true
is_trivially_move_assignable_v<...>      // yields false
```

```cpp
static_assert(is_swappable_with<T1, T2>);
static_assert(!is_nothrow_swappable_with<T1, T2>);
```

1.  如果类型 T 的表达式可以与类型 U 的表达式交换，则值为 true；否则为 false。该表达式在未求值上下文中是良构的。如果……，则两个类型 T 和 U 是可交换的。

    -   要求给定类型要么是完整类型（第 3.3 节），要么是未知边界的数组。
    -   注意，如果 T 或 U 是非引用、非数组类型，则 `is_swappable_with<T, U>` 总是产生 false，因为这类类型会产生右值。

    例如：

    ```cpp
    is_swappable_with<int, int> // yields false
    is_swappable_with<int&, int&> // yields true
    is_swappable_with<int&&, int&&> // yields true
    is_swappable_with<int&, int> // yields false
    is_swappable_with<int, int&> // yields false
    is_swappable_with<int&&, int&> // yields false
    is_swappable_with<int, int&&> // yields false
    is_swappable_with<int&, int&&> // yields true
    is_swappable_with<int&&, int> // yields false
    is_swappable_with<std::pair<int,int>, std::pair<int,int>> // yields true
    is_swappable_with<std::pair<int,int>&, std::pair<int,int>&> // yields true
    is_swappable_with<std::pair<int,int>, std::pair<int,int>&> // yields false
    is_swappable_with<std::pair<int,int>&, std::pair<int,int>> // yields false
    is_swappable_with<std::pair<int,int>&&, std::pair<int,int>&&> // yields true
    is_swappable_with<std::pair<int,int>&&, std::pair<int,int>&> // yields false
    is_swappable_with<std::pair<int,int>&, std::pair<int,int>&&> // yields false
    is_swappable_with<std::pair<int,int>&&, std::pair<int,int>> // yields false
    is_swappable_with<std::pair<int,int>, std::pair<int,int>&&> // yields false
    ```

    自 C++17 起可用。

```cpp
template< class T, class U >
struct is_nothrow_swappable_with;
```

2.  如果类型 T 的表达式可以与类型 U 的表达式交换，并且交换表达式为 `noexcept`，则值为 true；否则为 false。该表达式在未求值上下文中是良构的。如果……，则两个类型 T 和 U 是可交换的。

    -   要求给定类型要么是完整类型（第 3.3 节），要么是未知边界的数组。
    -   注意，如果 T 或 U 是非引用、非数组类型，则 `is_nothrow_swappable_with<T, U>` 总是产生 false，因为这类类型会产生右值。

    例如：

    ```cpp
    is_nothrow_swappable_with<int, int> // yields false
    is_nothrow_swappable_with<int&, int&> // yields true
    is_nothrow_swappable_with<int&&, int&&> // yields true
    is_nothrow_swappable_with<int&, int> // yields false
    is_nothrow_swappable_with<int, int&> // yields false
    is_nothrow_swappable_with<int&&, int&> // yields false
    is_nothrow_swappable_with<int, int&&> // yields false
    is_nothrow_swappable_with<int&, int&&> // yields true
    is_nothrow_swappable_with<int&&, int> // yields false
    is_nothrow_swappable_with<std::pair<int,int>, std::pair<int,int>> // yields true
    is_nothrow_swappable_with<std::pair<int,int>&, std::pair<int,int>&> // yields true
    is_nothrow_swappable_with<std::pair<int,int>, std::pair<int,int>&> // yields false
    is_nothrow_swappable_with<std::pair<int,int>&, std::pair<int,int>> // yields false
    ```

    自 C++17 起可用。

### D.3.2 类型之间的关系

表 D-3 列出了允许测试类型之间特定关系的类型萃取。这包括检查为类类型提供了哪些构造函数和赋值运算符。

```cpp
is_convertible_v<...>                 // yields false
```

-   要求给定类型要么是完整的（见第 [basic.types] 节），要么是未知边界的数组。
-   注意，const 指针是 const 限定类型，而指向 const 类型的非 const 指针或引用不是 const 限定的。例如，`is_assignable<...>` 对三种实例化模式具有不同的顺序。
-   实现细节见第 425 页的第 [..] 节。

## D.4 类型构造

表 D.6 中列出的萃取允许我们从其他类型构造类型。

| 萃取 | 效果 |
|---|---|
| `remove_const<T>` | 对应的不带 `const` 的类型 |
| `remove_volatile<T>` | 对应的不带 `volatile` 的类型 |
| `remove_cv<T>` | 对应的不带 `const` 和 `volatile` 的类型 |
| `add_const<T>` | 对应的 `const` 类型 |
| `add_volatile<T>` | 对应的 `volatile` 类型 |
| `add_cv<T>` | 对应的 `const volatile` 类型 |
| `make_signed<T>` | 对应的有符号非引用类型 |
| `make_unsigned<T>` | 对应的无符号非引用类型 |
| `remove_reference<T>` | 对应的非引用类型 |
| `add_lvalue_reference<T>` | 对应的左值引用类型（右值变为左值） |
| `add_rvalue_reference<T>` | 对应的右值引用类型（右值仍为右值） |
| `remove_pointer<T>` | 指针所指向的类型（否则为同一类型） |
| `add_pointer<T>` | 指向对应的非引用类型的指针类型 |
| `remove_extent<T>` | 数组的元素类型（否则为同一类型） |
| `remove_all_extents<T>` | 多维数组的元素类型（否则为同一类型） |
| `decay<T>` | 转换为对应的“按值”类型 |

表 D.6. 用于类型构造的萃取

`std::remove_const<T>::type`、`std::remove_volatile<T>::type` 和 `std::remove_cv<T>::type` 产生在顶层不带 const 和/或 volatile 的类型 T。

注意，const 指针是 const 限定类型，而指向 const 类型的非 const 指针或引用不是 const 限定的。例如：

```cpp
std::remove_const_t<const int>        // yields int
std::remove_const_t<const int*>       // yields const int*
std::remove_const_t<int const&>       // yields int const&
```

相反，我们可能更倾向于使用 `std::decay<>`，但它也会将数组类型和函数类型转换为对应的指针类型（见第 115 页的第 5.4 节）。

```cpp
std::decay_t<const T>            // yields int
std::decay_t<const T&>           // yields int
```

-   实现细节见第 696 页的第 9.3.2 节。

`std::add_const_t<T>`、`std::add_volatile_t<T>` 和 `std::add_cv_t<T>` 在顶层添加相应的 const/volatile 限定符。将其中一个萃取应用于引用类型或函数类型没有效果。例如：

```cpp
std::add_const_t<int>       // yields int const
std::add_const_t<volatile int> // yields int const volatile
std::add_const_t<int const>   // yields int const
std::add_const_t<int&>        // yields int&
std::add_const_t<int&&>       // yields int&&
std::add_const_t<int*>        // yields int* const
```

`std::make_signed_t<T>` 和 `std::make_unsigned_t<T>` 产生 T 对应的有符号/无符号类型。这要求 T 是枚举类型或除 bool 以外的（带 cv 限定的）整型类型。所有其他类型都会导致未定义行为（关于如何避免此类未定义行为的讨论，见第 696 页的第 9.3 节）。

```cpp
std::make_signed_t<char>        // yields signed char
std::make_unsigned_t<char>      // yields unsigned char
std::make_unsigned_t<char const> // yields unsigned char const
```

`std::remove_reference_t<T>` 产生引用类型 T 所引用的类型（如果 T 不是引用类型，则为 T 本身）。例如：

```cpp
std::remove_reference_t<int>         // yields int
std::remove_reference_t<int&>        // yields int
std::remove_reference_t<int&&>       // yields int
std::remove_reference_t<int const&>  // yields int const
std::remove_reference_t<int const&&> // yields int const
```

注意，引用类型本身不是 const 限定的。因此，`remove_const_t<int const&>` 的成员 `type` 是 `int const&`。

```cpp
std::remove_const_t<std::remove_reference_t<int const&>> // yields int
std::remove_reference_t<std::remove_const_t<int const&>> // yields int const
```
