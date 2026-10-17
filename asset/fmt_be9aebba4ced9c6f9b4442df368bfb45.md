
```
// 示例结束
```

## 16.4.4.4 `Cpp17Nullablepointer`

`Cpp17NullablePointer` 是一种具有可交换值的指针类类型。`P` 满足 `Cpp17NullablePointer` 要求，如果 `P` 满足 `Cpp17EqualityComparable`、`Cpp17DefaultConstructible`、`Cpp17CopyConstructible`，且：
- `P` 的可交换值满足 `Cpp17NullablePointer` 要求，
- `P` 在表 33 中的所有操作都是有效的 (7.3)，
- `P` 的值初始化对象满足 `Cpp17Destructible` 的要求。[注释 1：涉及不确定值的操作会导致未定义行为。—— 注释结束]
- `P` 的值初始化结果应当等价于自身。
- `P` 的值初始化对象具有不确定值。
- `P` 满足 `Cpp17NullablePointer` 要求。
- `u` 是一个整数。
- 在表 33 中，`t` 表示类型为（可能为 const）`P` 的值。
- `P` 可以转换为 `nullptr_t`。

## 16.4.4.5 `Cpp17Hash` 要求

1 `A` 满足 `Cpp17Hash` 要求，如果：
- 它是一个函数对象 (20.14)。

### 表 33：`Cpp17NullablePointer` 要求

| 表达式 | 返回类型 | 操作语义 |
|---|---|---|
| `P u(np);` | | 后置条件：`u == nullptr` |
| `P = np;` | | |
| `P(np)` | | 后置条件：`P(np) == nullptr` |
| `a != b` | 可转换为 bool | `!(a == b)` |
| `a = np` | 可转换为 bool | `a == P()` |
| `np = a` | 可转换为 bool | `!(a == b)` |

### 表 34：`Cpp17Hash` 要求

| 表达式 | 返回类型 |
| ------|---|
| `h(k)` | `size_t` | 返回的值在程序运行期间仅取决于参数 `k`。[注释：对于给定的程序执行，相同的 `h(x)` 产生相同的结果。] 对于不同的值 `t1` 和 `t2`，`h(t1)` 和 `h(t2)` 相等的概率非常小，接近 `1.0 / numeric_limits<size_t>::max()`。 |
| `h(u)` | `size_t` | 不修改。 |

## 16.4.4.6 `Cpp17Allocator` 要求

### 16.4.4.6.1 通用

库提供了分配器的规则，分配器是封装分配模型的类类型对象。这些信息包括指针类型、它们的差异类型、分配模型中对象的大小，以及基本类型的内存分配和释放。所有的字符串（第21节）、常量（第22节，除数组外）、字符串缓冲区和流（第29节）以及匹配结果（第30节）都根据分配器参数化。

`class allocator_traits` (20.10.9) 为所有分配器类型提供了统一接口。表 35 描述了分配器类型的要求以及如何实例化 `allocator_traits`。如果表 36 的最后一列为给表达式定义了默认值，则该要求是可选的。`allocator_traits` 的用户特化可以提供不同的函数，并针对不同要求提供主模板不同的默认值。在表 35 和表 36 中，`move` 和 `forward` 的使用始终指的是 `std::move` 和 `forward`。

### 表 36：`Cpp17Allocator` 要求

| 表达式 | 返回类型 | 断言/注释 | 默认值 |
|---|---|---|---|
| `X::pointer` | | 前置/后置条件 | `T*` |

# ISO/IEC 14882:2020(E)

## 表 36: `Cpp17Allocator` 节点（续）

| 表达式 | 返回类型 | 断言/注前提/后置条件 | 默认值 |
| --- | --- | --- | --- |
| `X::const_pointer` | | `X::pointer` 可转换为 `X::const_pointer` | `pointer_traits<X>::pointer_rebind<const T>` |
| `X::void_pointer` `Y::void_pointer` | | `X::pointer` 可转换为 `X::void_pointer` 且 `X::void_pointer` 与 `Y::void_pointer` 是同一种类型。 | `pointer_traits<X>::pointer_rebind<void>` |
| `X::const_void_pointer` `Y::const_void_pointer` | | `X::pointer`, `X::const_pointer` 和 `X::void_pointer` 均可转换为 `X::const_pointer`。`X::void_pointer` 与 `Y::void_pointer` 是同一种类型。 | `pointer_traits<X>::pointer_rebind<const>` |
| `X::value_type` `X::size_type` | 等于 `T` 的无整数类型 | 能够表示分配模型中最大对象大小的类型 | `make_unsigned<T>::difference_type` |
| `X::difference_type` | 有符号整数类型 | 能够表示分配模型中两个指针差值的类型 | `pointer_traits<X>::difference_type` |
| `typename X::template rebound<U>::other` | `Y` | 对于所有 `U`（包括 `T`），`Y::template rebound<>::other` 是 `X`。 | 参见下文注 A。 |
| `*q` | `const T&` | `*q` 指向与 `*p` 相同的对象。 | |
| `p->m` | `T` 的类型 | 前置条件：`(*p).m` 是定义的。等同于 `(*p).m` | |
| `q->m` | `T` 的类型 | 前置条件：`(*q).m` 是定义的。等同于 `(*q).m` | |
| `static_cast<X::pointer>(w)` | `X::pointer` | `static_cast<X::pointer>(w) == p` | |
| `static_cast<X::const_pointer>(x)` | `X::const_pointer` | `static_cast<X::const_pointer>(x) == q` | |
| `pointer_traits<X::pointer>::pointer_to(r)` | `X::pointer` | 同于 `p` | |

## 表 36: `Cpp17Allocator` 节点（续）

| 表达式 | 返回类型 | 断言/注前提/后置条件 | 默认值 |
|--- | --- | --- | --- |
| `a.allocate(n)` | `X::pointer` | 为 `n` 个 `T` 分配内存。<br><br>[示例 1：由指针值 `p` 表示的存储可以使用 `static_cast<T>(new (p) sizeof(T)))` 来隐式创建一个数组并获取其指针。<br>- 结束示例> `allocate` 可能会抛出异常<br>[注 1：如果 `n == 0` 则值未定义。结束注] | |
| `a.allocate(n, y)` | `X::pointer` | 同于 `a.allocate(n)`。`y` 的使用是未定义的。 | `a.allocate(n)` |
| `a.deallocate(p,n)` | (未使用) | 前置条件：`p` 是早先调用 `allocate` 返回的值且未被中间的 `deallocate` 调用失效。<br><br>抛出：无。 | |
| `a.max_size()` | `X::size_type` | 有意义地传递给 `X::allocate()` 的最大值 | `numeric_limits<size_type>::max()` |
| `a1 == a2` | `bool` | 仅当分配分配的存储可以通过运算符处理时返回 true；运算符具有自反性、对称性和传递性，且不抛出异常。同于 `a1 == a2` | |
| `a1 != a2` | `bool` | 同于 `a1 != a2` | |
| `a === b` | `bool` | 同于 `a === b` | |
| `a = b` | `bool` | `Y::rebinit<T>::other(b)`<br>同于 `a = b)`<br>不抛出异常。后置条件：`u = a` | |
| `X u(a);` | | 不抛出异常。后置条件：`Y(u) = b, u = X(b)` | |
| `X u(std::move(a));` | | | |
| `X u = std::move(a);` | | 不抛出异常。后置条件：`a` 的值不变且等于 `u`。 | |
| `X u(std::move(b));` | | | |
| `X u(b);` | | 不抛出异常。后置条件：`u` 等于 `X(b)` 的先前值。 | |

当 `sizeof(T)` 较小时，`a.allocate` 是分配单个类型 `T` 对象的有效手段。容器不需要维护自己的。

## 表 36: `Cpp17Allocator` 节点（续）

| 表达式 | 返回类型 | 断言/后置条件 | 默认值 |
|---|---|---|---|
| `a.construct(c, args)` | (未使用) | 影响：在 `c` 处构造类型为 `C` 的对象 | `construct(c, std::forward<Args>(args))` |
| `a.destroy(c)` | (未使用) | 影响：销毁 `c` 处的对象。通常返回 `a` 或 `X()`。 | `return a;` |
| `a.select_on_container_construction()` | `X` | 同于 `true_type`；当容器拷贝赋值时拷贝 `X` 的分配器时返回 `true_type`。参见注 B。 | `false_type` |
| `X::propagate_on_container_copy_assignment()` | 同于 `true_type` 或 `false_type` | 当容器移动赋值时应移动 `X` 的分配器时返回 `true_type`。参见注 B。 | `false_type` |
| `X::propagate_on_container_swap()` | 同于 `true_type` 或 `false_type` | 当容器交换时应交换 `X` 的分配器时返回 `true_type`。参见注 B。 | `false_type` |
| `X::is_equal()` | 同于 `true_type` 或 `false_type` | 对于类型为 `X` 的可能的值 `a1, a2`，表达式 `a1 == a2` 保证为真时返回 `true_type`。 | `is_empty<X>::type` |

注 3：表中的成员类模板 `rebind` 是 typedef。
注 2：通常，如果名称 `Allocator` 绑定到 `SomeAllocator`，则 `Allocator::rebind::other` 是另一种类型，其中 `SomeAllocator::value_type` 是 `T` 且 `SomeAllocator<U>::value_type` 是 `U`。如果 `Allocator` 是类模板 `Alloc<T, Args>`，其中 `Args` 是零个或多个参数，且 `Allocator` 未提供 `rebind` 模板，则 `allocator_traits` 使用 `rebind` 代替 `Allocator::rebind::other`。对于不是分配器的其他类型，不提供默认值。

注 4：如果 `X::propagate_on_container_copy_assignment::value` 为 true，`X` 应满足 `Cpp17_Assignable` 要求（表 31）且该操作不抛出异常。如果 `X::propagate_on_container_move_assignment::value` 为 true，`X` 必须满足 `Cpp17_Assignable` 要求。如果 `X::propagate_on_container_swap::value` 为 true，值应为类型 `X` 且交换操作不抛出异常。

注 5：分配器应满足 `Cpp17_Constructible` 要求（表 29）。`X::pointer`, `X::const_pointer`, `X::void_pointer` 和 `X::const_void_pointer` 还满足 `Cpp17_NavigablePointer`（表 33）以及对于整数值 `n`，`a + n == address(a) + n` 为真的额外要求。

让 `x1` 和 `x2` 代表（可能不同的）类型：`X::void_pointer`, `X::const_void_pointer`, `X::pointer` 和 `X::const_pointer`。则 `x1` 和 `x2` 是等值的指针，且如果只有 `x1` 和 `x2` 能够显式转换为对应的对象 `px1` 和 `px2` 类型 `X::const-`

## 表 35: 描述性变量定义

| 变量 | 定义 |
|---|---|
| `T, U, C` | 任意未对齐对象类型（6.8）的分配器类 |
| `V` | `U` 的对应分配器类 |
| `XX` | 类型 `allocator_traits<X>` 或 `allocator_traits<Y>` |
| `a, a1, a2` | 类型的值 |
| `u` | 声明的变量名称 |
| `b` | 类型 `p` 的值 |
| `c` | 指接有效的类型 `C` 指针 |
| `p` | 类型 `XX::pointer` 的值，通过调用 `ai` 获取，其中 `ai = a` |
| `q` | 通过值 `p` 转换得到的类型 `XX::const_pointer` |
| `r` | 通过表达式 `*p` 获得的 `T&` |
| `w` | 类型 `XX::void_pointer` 的值，通过值 `p` 转换 |
| `x` | 通过值 `q` 或值 `w` 转换得到的类型 `XX::const_pointer` |
| `n` | `XX::size_type` 的值 |
| `Args` | 模板参数包 |
| `args` | 模式为 `Args&&` 的函数包 |

```cpp
template<class Tp>
struct SimpleAllocator {
  typedef Tp value_type;
  SimpleAllocator(const* args);
  template<class T> SimpleAllocator(const SimpleAllocator<T>& other);
  [[nodiscard]] Tp* allocate(std::size_t n);
  void deallocate(Tp* p, std::size_t n);
};
template<class T, class U>
bool operator===(const SimpleAllocator<T>&, const SimpleAllocator<U>&);
template<class T, class U>
bool operator!=(const SimpleAllocator<T>&, const SimpleAllocator<U>&);
```
