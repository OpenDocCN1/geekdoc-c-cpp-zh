

```
is_assignable_v<std::string&&, std::string&&> // yields true
```

## std:: **is_copy_assignable** < T >::value
std:: **is_trivially_copy_assignable** < T >::value
std:: **is_nothrow_copy_assignable** < T >::value

- 如果类型 T 的值可以赋给类型 T 的对象，则返回 true（不使用非平凡操作或保证不抛出异常）。
- 如果 T 不是 *可引用类型*，则返回 `false`（即 (cv-限定) `void` 或带有 `const`、`volatile`、`&` 和/或 `&&` 限定的函数类型）。
- 只要 T 是可引用类型，则分别与 `is_assignable<T&, T const&>::value`、`is_trivially_assignable<T&, T const&>::value` 或 `is_nothrow_assignable<T&, T const&>::value` 相同。
- 要判断类型 T 的右值是否可以赋给另一个类型 T 的右值，请使用 `is_assignable<T&&, T&&>`，依此类推。
- 请注意，`void`、内置数组类型以及拷贝赋值运算符被删除的类不能进行拷贝赋值。
- 要求给定的类型是完整的（参见第 10.3.1 节第 154 页）、(cv-限定) `void`，或未知边界的数组。
- 例如：

[Click here to view code image](#)

```
is_copy_assignable_v<int> // yields true
is_copy_assignable_v<int&> // yields true
is_copy_assignable_v<int&&> // yields true
is_copy_assignable_v<void> // yields false
is_copy_assignable_v<void*> // yields true
is_copy_assignable_v<char[]> // yields false
is_copy_assignable_v<std::string> // yields true
is_copy_assignable_v<std::unique_ptr<int>> // yields false
```

## std:: **is_move_assignable** < T >::value
std:: **is_trivially_move_assignable** < T >::value
std:: **is_nothrow_move_assignable** < T >::value

- 如果类型 T 的右值可以移动赋给类型 T 的对象，则返回 true（不使用非平凡操作或保证不抛出异常）。
- 如果 T 不是 *可引用类型*，则返回 `false`（即 (cv-限定) `void` 或带有 `const`、`volatile`、`&` 和/或 `&&` 限定的函数类型）。
- 只要 T 是可引用类型，则分别与 `is_assignable<T&, T&&>::value`、`is_trivially_assignable<T&, T&&>::value` 或 `is_nothrow_assignable<T&, T&&>::value` 相同。
- 请注意，`void`、内置数组类型以及移动赋值运算符被删除的类不能进行移动赋值。
- 要求给定的类型是完整的（参见第 10.3.1 节第 154 页）或 (cv-限定) `void` 或未知边界的数组。
- 例如：

[Click here to view code image](#)

```
is_move_assignable_v<int> // yields true
is_move_assignable_v<int&> // yields true
is_move_assignable_v<int&&> // yields true
is_move_assignable_v<void> // yields false
is_move_assignable_v<void*> // yields true
is_move_assignable_v<char[]> // yields false
is_move_assignable_v<std::string> // yields true
is_move_assignable_v<std::unique_ptr<int>> // yields true
```

## `std::is_destructible<T>::value`

`std::is_trivially_destructible<T>::value`

`std::is_nothrow_destructible<T>::value`

- 如果类型 T 的对象可以被销毁，则返回 `true`（不使用非平凡操作或保证不抛出异常）。
- 对引用始终返回 `true`。
- 对 `void`、未知边界的数组类型和函数类型始终返回 `false`。
- `is_trivially_destructible` 如果 T 的析构函数、任何基类或任何非静态数据成员未被用户定义或为虚函数，则返回 `true`。
- 要求给定的类型是完整的（参见第 10.3.1 节第 154 页）、(cv-限定) `void`，或未知边界的数组。
- 例如：

[Click here to view code image](#)

```
is_destructible_v<void> // yields false
is_destructible_v<int> // yields true
is_destructible_v<std::string> // yields true
is_destructible_v<std::pair<int,std::string>> // yields true
```

```
is_trivially_destructible_v<void> // yields false
is_trivially_destructible_v<int> // yields true
is_trivially_destructible_v<std::string> // yields false
is_trivially_destructible_v<std::pair<int,int>> // yields true
is_trivially_destructible_v<std::pair<int,std::string>> // yields false
```

## std:: is_swappable_with < T1, T2 >::value
std:: is_nothrow_swappable_with < T1, T2 >::value

- 如果类型 T1 的表达式可以与类型 T2 的表达式进行 swap()，则返回 true，除非引用类型仅决定表达式的值类别（并保证不抛出异常）。
- 要求给定的类型是完整的（参见第 10.3.1 节第 154 页）、(cv-限定) void，或未知边界的数组。
- 请注意，对于第一个或第二个类型为非引用、非类类型的 is_swappable_with_v<> 始终返回 false，因为此类类型会产生纯右值。即 swap(42,77) 无效。
- 例如：

Click here to view code image

```
is_swappable_with_v<int,int> // yields false
is_swappable_with_v<int&,int> // yields false
is_swappable_with_v<int&&,int> // yields false
is_swappable_with_v<int&,int&> // yields true
is_swappable_with_v<int&&,int&&> // yields false
is_swappable_with_v<int&,long&> // yields false
is_swappable_with_v<int&,void*> // yields false
is_swappable_with_v<void*,int> // yields false
is_swappable_with_v<void*,int&> // yields false
is_swappable_with_v<std::string,std::string> // yields false
is_swappable_with_v<std::string&,std::string&> // yields true
is_swappable_with_v<std::string&&,std::string&&> // yields false
```

- 自 C++17 起可用。

## std:: is_swappable < T >::value
std:: is_nothrow_swappable < T >::value

- 如果类型 T 的左值可以被交换，则返回 true（并保证不抛出异常）。
- 只要 T 是可引用类型。分别与 is_swappable_with<T&,T&>::value 或 is_nothrow_swappable_with<T&,T&>::value 相同。
- 如果 T 不是可引用类型，则返回 false（即 (cv-限定) void 或带有 const、volatile、& 和/或 && 限定的函数类型）。
- 要判断类型 T 的右值是否可以与另一个类型 T 的右值交换，请使用 is_swappable_with<T&&, T&&>。
- 要求给定的类型是完整类型（第 10.3.1 节第 154 页）、(cv-限定) void，或未知边界的数组。
- 例如：

Click here to view code image

```
is_swappable_v<int> // yields true
is_swappable_v<int&> // yields true
is_swappable_v<int&&> // yields true
is_swappable_v<std::string&&> // yields true
is_swappable_v<void> // yields false
is_swappable_v<void*> // yields true
is_swappable_v<char[]> // yields false
is_swappable_v<std::unique_ptr<int>> // yields true
```

- 自 C++17 起可用。

## D.3.3 Relationships Between Types

表 D.5 列出了允许测试类型之间某些关系的类型特征。这包括检查为类类型提供的构造函数和赋值运算符。

| Trait | Effect |
|---|---|
| is_same<T1, T2> | T1 和 T2 是相同的类型（包括 const/volatile 限定符） |
| is_base_of<T, D> | 类型 T 是类型 D 的基类 |
| is_convertible<T, T2> | 类型 T 可转换为类型 T2 |

表 D.5. 用于测试类型关系的特征

```
std:: is_same < T1, T2 > ::value
```

- 如果 T1 和 T2 命名相同的类型，包括 cv-限定符（const 和 volatile），则返回 true。
- 如果一个类型是另一个类型的类型别名，则返回 true。
- 如果两个对象由相同类型的对象初始化，则返回 true。
- 对于两个不同 lambda 表达式关联的（闭包）类型，即使它们定义相同的行为，也返回 false。
- 例如：

Click here to view code image

```
auto a = nullptr;
auto b = nullptr;
is_same_v<decltype(a),decltype(b)> // yields true

using A = int;
is_same_v<A,int> // yields true

auto x = [] (int) {};
auto y = x;
auto z = [] (int) {};
is_same_v<decltype(x),decltype(y)> // yields true
is_same_v<decltype(x),decltype(z)> // yields false
```

- 有关实现细节，请参见第 19.3.3 节第 410 页。

## std:: is_base_of < B, D > ::value

- 如果 B 是 D 的基类或 B 与 D 是同一类，则返回 true。
- 是否使用 cv-限定、private 或 protected 继承、D 是否有多个类型为 B 的基类，或 D 是否通过多继承路径（通过虚继承）将 B 作为基类，都无关紧要。
- 如果至少一个类型是联合体，则返回 false。
- 要求类型 D 是完整的（参见第 10.3.1 节第 154 页）、与 B 具有相同类型（忽略任何 const/volatile 限定），或既不是 struct 也不是 class。
- 例如：

Click here to view code image

```
class B {
};
class D1 : B {
}; class D2 : B {
}; class DD : private D1, private D2 {
};
is_base_of_v<B, D1> // yields true
is_base_of_v<B, DD> // yields true
is_base_of_v<B const, DD> // yields true
is_base_of_v<B, DD const> // yields true
is_base_of_v<B, B const> // yields true
is_base_of_v<B&, DD&> // yields false (no class type)
is_base_of_v<B[3], DD[3]> // yields false (no class type)
```
