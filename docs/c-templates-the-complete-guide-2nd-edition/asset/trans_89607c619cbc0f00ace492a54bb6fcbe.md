

- 具有此属性的对象可以通过哈希关联的字节序列来产生可靠的哈希值（不存在某些不参与对象值的位在不同情况下可能不同的风险）。
- 要求给定的类型是可 trivially 复制的（参见第 D.3.1 节第 712 页）并且是完整的（参见第 10.3.1 节第 154 页）或（cv-限定）void 或未知边界的数组。
- 自 C++17 起可用。

## std::alignment_of<T>::value

- 给出类型 T 的对象的对齐值作为 std::size_t（对于数组，为元素类型；对于引用，为被引用类型）。
- 与：alignof(T) 相同
- 该 trait 在 C++11 中引入，早于 alignof(...) 构造。然而它仍然有用，因为该 trait 可以作为类类型传递，这对于某些元程序很有用。
- 要求 alignof(T) 是一个有效的表达式。
- 使用 aligned_union<> 来获取多个类型的共同对齐（参见第 D.5 节第 733 页）。

## std::rank<T>::value

- 给出类型 T 的数组的维度数作为 std::size_t。
- 对于所有其他类型给出 0。
- 指针没有任何关联的维度。数组类型中的未指定边界确实指定了一个维度。（通常，函数参数声明为数组类型时并不具有实际的数组类型，并且 std::array 也不是数组类型。参见第 D.2.1 节第 704 页。）例如：

```
int a2[5][7];
rank_v<decltype(a2)>; // yields 2
rank_v<int*>; // yields 0 (no array)
extern int p1[];
rank_v<decltype(p1)>; // yields1
```

## std::extent<T>::value
std::extent<T, IDX>::value

- 给出类型 T 的数组的第一个或 IDX-th 维度的大小作为 std::size_t。
- 如果 T 不是数组、维度不存在或大小的
- 有关实现细节，请参见第 19.8.2 节第 453 页。

```
int a2[5][7];
extent_v<decltype(a2)>; // yields 5
extent_v<decltype(a2),0>; // yields 5
extent_v<decltype(a2),1>; // yields 7
extent_v<decltype(a2),2>; // yields 0
extent_v<int*>; // yields 0
extent_v<int p[1]>;
extent_v<decltype(p1)>; // yields 0
```

## std::underlying_type<T>::type

- 给出枚举类型 T 的底层类型。
- 要求给定的类型是完整的（参见第 10.3.1 节第 154 页）枚举类型。对于所有其他类型，它的行为未定义。

## std::is_invocable<T, Args...>::value
std::is_nothrow_invocable<T, Args...>::value

- 如果 T 可用作 Args... 的可调用对象（并保证不抛出异常）则给出 true。
- 也就是说，我们可以使用这些 trait 来测试是否可以调用或 std::invoke() 给定的可调用对象 T 用于 Args...（有关可调用对象和 std::invoke() 的详细信息，请参见第 11.1 节第 157 页）。要求所有给定的类型都是完整的（参见第 10.3.1 节第 154 页）或（cv-限定）void 或未知边界的数组。
- 例如：

```
struct C {
  bool operator() (int) const {
    return true;
  }
};
std::is_invocable<C>::value //false
std::is_invocable<C,int>::value //true
std::is_invocable<int*>::value //false
std::is_invocable<int(*)()>::value //true
```

- 自 C++17 起可用。

## std::is_invocable_r<RET_T, T, Args...>::value
std::is_nothrow_invocable_r<RET_T, T, Args...>::value

- 如果我们可以使用 T 作为 Args... 的可调用对象（并保证不抛出异常），返回可转换为类型 RET_T 的值，则给出 true。
- 也就是说，我们可以使用这些 trait 来测试是否可以调用或 std::invoke() 传递的可调用对象 T 用于 Args... 并将返回值用作 RET_T。（有关可调用对象和 std::invoke() 的详细信息，请参见第 11.1 节第 157 页。）
- 要求所有传递的类型都是完整的（参见第 10.3.1 节第 154 页）或（cv-限定）void 或未知边界的数组。
- 例如：

```
struct C {
bool operator() (int) const {
return true;
}
};
std::is_invocable_r<bool,C,int>::value //true
std::is_invocable_r<int,C,long>::value //true
std::is_invocable_r<void,C,int>::value //true
std::is_invocable_r<char*,C,int>::value //false
std::is_invocable_r<long,int(*)(int)>::value //false
std::is_invocable_r<long,int(*)(int),int>::value //true
std::is_invocable_r<long,int(*)(int),double>::value //true
```

- 自 C++17 起可用。

## std::invoke_result<T, Args...>::value
std::result_of<T, Args...>::value

- 给出可调用对象 T 被调用用于 Args.... 的返回类型。
- 请注意语法略有不同：– 要使用 invoke_result<>，你必须将可调用对象的类型和参数的类型作为参数传递。
- – 要使用 result_of<>，你必须使用相应的类型传递一个“函数声明”。
- 如果无法调用，则未定义类型成员，因此使用它会出错（这可能会使使用它在声明中进行 SFINAE 的函数模板失效；参见第 8.4 节第 131 页）。
- 也就是说，我们可以使用这些 trait 来获取调用或 std::invoke() 给定的可调用对象 T 用于 Args.... 时获得的返回类型。（有关可调用对象和 std::invoke() 的详细信息，请参见第 11.1 节第 157 页。）
- 要求所有给定的类型都是完整的（参见第 10.3.1 节第 154 页），（cv-

- `invoke_result<>` 自 C++17 起可用并取代 `result_of<>`，后者自 C++17 起已弃用，因为 `invoke_result<>` 提供了一些改进，例如更简单的语法和允许 T 为抽象类型。
- 例如：

```
std::string foo(int);

using R0 = typename std::result_of<decltype(&foo)(int)>::type; // C++11
using R1 = std::result_of_t<decltype(&foo)(int)>; // C++14
using R2 = std::invoke_result_t<decltype(foo), int>; // C++17

struct ABC {
virtual ~ABC() = 0;
void operator() (int) const {
}
};

using T1 = typename std::result_of<ABC(int)>::type; // ERROR: ABC is abstract
using T2 = typename std::invoke_result<ABC, int>::type; // OK since C++17
```

请参见第 11.1.3 节第 163 页的完整示例。

## D.3.2 Test for Specific Operations

| Trait | Effect |
|---|---|
| `is_constructible<T, Args...>` | 可以使用类型 *Args* 初始化类型 *T* |
| `is_trivially_constructible<T, Args...>` | 可以 trivially 使用类型 *Args* 初始化类型 *T* |
| `is_nothrow_constructible<T, Args...>` | 可以使用类型 *Args* 初始化类型 *T* 且该操作不会抛出 |
| `is_default_constructible<T>` | 可以在不带参数的情况下初始化 *T* |
| `is_trivially_default_constructible<T>` | 可以 trivially 在不带参数的情况下初始化 T |
| `is_nothrow_default_constructible<T>` | 可以在不带参数的情况下初始化 T 且该操作不会抛出 |
| `is_copy_constructible<T>` | 可以复制一个 T |
| `is_trivially_copy_constructible<T>` | 可以 trivially 复制一个 T |
| `is_nothrow_copy_constructible<T>` | 可以复制一个 T 且该操作不会抛出 |
| `is_move_constructible<T>` | 可以移动一个 T |
| `is_trivially_move_constructible<T>` | 可以 trivially 移动一个 T |
| `is_nothrow_move_constructible<T>` | 可以移动一个 T 且该操作不会抛出 |
| `is_assignable<T, T2>` | 可以将类型 T2 分配给类型 T |
| `is_trivially_assignable<T, T2>` | 可以 trivially 将类型 T2 分配给类型 T |
| `is_nothrow_assignable<T, T2>` | 可以将类型 T2 分配给类型 T 且该操作不会抛出 |
| `is_copy_assignable<T>` | 可以复制赋值一个 T |
| `is_trivially_copy_assignable<T>` | 可以 trivially 复制赋值一个 T |
| `is_nothrow_copy_assignable<T>` | 可以复制赋值一个 T 且该操作不会抛出 |
| `is_move_assignable<T>` | 可以移动赋值一个 T |
| `is_trivially_move_assignable<T>` | 可以 trivially 移动赋值一个 T |
| `is_nothrow_move_assignable<T>` | 可以移动赋值一个 T |

|  |  |
|---|---|
| `is_destructible<T>` | 可以销毁一个 *T* |
| `is_trivially_destructible<T>` | 可以 trivially 销毁一个 *T* |
| `is_nothrow_destructible<T>` | 可以 trivially 销毁一个 *T* 且该操作不会抛出 |
| `is_swappable<T>` | 可以为此类型调用 `swap()`（自 C++17 起） |
| `is_nothrow_swappable<T>` | 可以为此类型调用 `swap()` 且该操作不会抛出（自 C++17 起） |
| `is_swappable_with<T, T2>` | 可以为这两个类型调用 `swap()`，具有特定的值类别（自 C++17 起） |
| `is_nothrow_swappable_with<T, T2>` | 可以为这两个类型调用 `swap()`，具有特定的值类别且该操作不会抛出（自 C++17 起） |

*Table D.4. Traits to Check for Specific Operations*

表 D.4 列出了允许我们检查某些特定操作的 type traits。带有 `is_trivially_...` 的形式 additionally 检查为对象、成员或基类调用的所有（子）操作是否都是 trivial（既非用户定义也非虚）。带有 `is_nothrow_...` 的形式 additionally 检查所调用的操作是否保证不抛出。请注意，所有 `is_..._constructible` 检查都隐含了相应的 `is_..._destructible` 检查。例如：

```
utils/isconstructible.cpp
```
