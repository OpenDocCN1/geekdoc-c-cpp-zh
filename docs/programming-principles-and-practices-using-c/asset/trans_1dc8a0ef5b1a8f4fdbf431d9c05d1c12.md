
## B.5.7 排列

| 函数 | 描述 |
| :--- | :--- |
| `x = next_permutation(b, e)` | 将 `b:e` 调整为字典序中的下一个排列。 |
| `x = next_permutation(b, e, f)` | 使用 `f` 进行比较，将 `b:e` 调整为字典序中的下一个排列。 |
| `x = prev_permutation(b, e)` | 将 `b:e` 调整为字典序中的上一个排列。 |
| `x = prev_permutation(b, e, f)` | 使用 `f` 进行比较，将 `b:e` 调整为字典序中的上一个排列。 |

对于 `next_permutation`，如果 `b:e` 已经包含最后一个排列（例如示例中的 `cba`），则其返回值 (`x`) 为 `false`；在这种情况下，它返回第一个排列（例如示例中的 `abc`）。对于 `prev_permutation`，如果 `b:e` 已经包含第一个排列（例如示例中的 `abc`），则其返回值为 `false`；在这种情况下，它返回最后一个排列（例如示例中的 `cba`）。

## B.5.8 min 和 max

值比较在许多上下文中都非常有用：

### min 和 max

| 函数 | 描述 |
| :--- | :--- |
| `x = max(a, b)` | `x` 是 `a` 和 `b` 中较大的一个。 |
| `x = max(a, b, f)` | 使用 `f` 进行比较，`x` 是 `a` 和 `b` 中较大的一个。 |
| `x = max({elems})` | `x` 是 `{elems}` 中的最大元素。 |
| `x = max({elems}, f)` | 使用 `f` 进行比较，`x` 是 `{elems}` 中的最大元素。 |
| `x = min(a, b)` | `x` 是 `a` 和 `b` 中较小的一个。 |
| `x = min(a, b, f)` | 使用 `f` 进行比较，`x` 是 `a` 和 `b` 中较小的一个。 |
| `x = min({elems})` | `x` 是 `{elems}` 中的最小元素。 |
| `x = min({elems}, f)` | 使用 `f` 进行比较，`x` 是 `{elems}` 中的最小元素。 |
| `pair(x, y) = minmax(a, b)` | `x` 是 `max(a, b)`，`y` 是 `min(a, b)`。 |
| `pair(x, y) = minmax(a, b, f)` | `x` 是 `max(a, b, f)`，`y` 是 `min(a, b, f)`。 |
| `pair(x, y) = minmax({elems})` | `x` 是 `max({elems})`，`y` 是 `min({elems})`。 |
| `pair(x, y) = minmax({elems}, f)` | `x` 是 `max({elems}, f)`，`y` 是 `min({elems}, f)`。 |

### min 和 max（续）

| 函数 | 描述 |
| :--- | :--- |
| `p = max_element(b, e)` | `p` 指向 `[b, e)` 中的最大元素。 |
| `p = max_element(b, e, f)` | 使用 `f` 作为元素比较，`p` 指向 `[b, e)` 中的最大元素。 |
| `p = min_element(b, e)` | `p` 指向 `[b, e)` 中的最小元素。 |
| `p = min_element(b, e, f)` | 使用 `f` 作为元素比较，`p` 指向 `[b, e)` 中的最小元素。 |
| `lexicographical_compare(b, e, b2, e2)` | `[b, e) < [b2, e2]` 是否成立？ |
| `lexicographical_compare(b, e, b2, e2, f)` | 使用 `f` 作为元素比较，`[b, e) < [b2, e2]` 是否成立？ |

# B.6 STL 工具

标准库提供了一些机制，以简化标准库算法的使用。

## B.6.1 插入迭代器

通过迭代器向容器产生输出意味着迭代器所指向的元素及其后续元素可能会被覆盖。这也意味着可能会发生溢出以及随之而来的内存损坏。例如：

```cpp
void f(vector<int>& vi)
{
	fill_n(vi.begin(), 200, 7);	// 将 vi[0]..[199] 赋值给 7
}
```

如果 `vi` 的元素少于 200 个，我们就陷入了困境。

在 `<iterator>` 中，标准库提供了三个迭代器，通过向容器添加（插入）元素而不是覆盖旧元素来处理这个问题。提供了三个函数来生成这些插入迭代器：

### 插入迭代器

| 函数 | 描述 |
| :--- | :--- |
| `r = back_inserter(c)` | `*r = x` 会导致执行 `c.push_back(x)`。 |
| `r = front_inserter(c)` | `*r = x` 会导致执行 `c.push_front(x)`。 |
| `r = inserter(c, p)` | `*r = x` 会导致执行 `c.insert(p, x)`。 |

对于 `inserter(c, p)`，`p` 必须是容器 `c` 的有效迭代器。当然，每次通过插入迭代器向其写入值时，容器的大小都会增加一个元素。当写入发生时，插入器使用 `c.push_back(x)`、`c.push_front()` 或 `c.insert()` 将新元素插入到序列中，而不是覆盖现有元素。例如：

```cpp
void g(vector<int>& vi)
{
    fill_n(back_inserter(vi), 200, 7); // 在 vi 的末尾添加 200 个 7
}
```

## B.6.2 函数对象

许多标准算法接受函数对象（或函数）作为参数，以控制其工作方式。常见的用途包括比较准则、谓词（返回 `bool` 的函数）以及算术运算。在 `<functional>` 中，标准库提供了一些常用的函数对象。

### 谓词

| 函数 | 描述 |
| :--- | :--- |
| `p = equal_to<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x == y`。 |
| `p = not_equal_to<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x != y`。 |
| `p = greater<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x > y`。 |
| `p = less<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x < y`。 |
| `p = greater_equal<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x >= y`。 |
| `p = less_equal<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x <= y`。 |
| `p = logical_and<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x && y`。 |
| `p = logical_or<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x || y`。 |
| `p = logical_not<T>{}` | 当 `x` 为类型 `T` 时，`p(x)` 意味着 `!x`。 |

例如：

```cpp
vector<int> v; // ...
sort(v.begin(), v.end(), greater<int>{}); // 按降序对 v 进行排序
```

请注意，`logical_and` 和 `logical_or` 总是对其两个参数进行评估（而 `&&` 和 `||` 则不会）。

此外，lambda 表达式（§15.3.3）通常是简单函数对象的一个替代方案：

```cpp
sort(v.begin(), v.end(), [](int x, int y) { return x > y; });  // 按降序对 v 进行排序
```

### 算术运算

| 函数 | 描述 |
| :--- | :--- |
| `f = plus<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`f(x, y)` 意味着 `x + y`。 |
| `f = minus<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`f(x, y)` 意味着 `x - y`。 |
| `f = multiplies<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`f(x, y)` 意味着 `x * y`。 |
| `f = divides<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`f(x, y)` 意味着 `x / y`。 |
| `f = modulus<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`f(x, y)` 意味着 `x % y`。 |
| `f = negate<T>{}` | 当 `x` 为类型 `T` 时，`f(x)` 意味着 `-x`。 |

*更正说明：OCR 文本在 negate 中使用了 `~x`，但标准 C++ 的 `negate` 执行的是零减法，即 `-x`。鉴于算术运算的上下文，`~x` 很可能是 `-x` 的 OCR 错误，或者文本本意是位 NOT 但错误地使用了 `negate` 名称。然而，标准的 `std::negate` 是加法逆元。如果可能的话，让我们查看源代码。在《C++ 编程原理与实践》中，描述了 `negate`。实际上，查看 OCR，`~x` 显然是 `negate` 作为算术函子语境下 `-x` 的错字。我将把 `~x` 更正为 `-x`。*

### 适配器

| 函数 | 描述 |
| :--- | :--- |
| `f = bind(g, args)` | `f(x)` 意味着 `g(x, args)`，其中 `args` 可以是一个或多个参数。 |
| `f = mem_fun(mf)` | `f(p, args)` 意味着 `p->mf(args)`，其中 `args` 可以是一个或多个参数。 |
| `function<F> f {g}` | `f(args)` 意味着 `g(args)`，其中 `args` 可以是一个或多个参数。`F` 是 `g` 的类型。 |
| `f = not1(g)` | `f(x)` 意味着 `!g(x)`。 |
| `f = not2(g)` | `f(x, y)` 意味着 `!g(x, y)`。 |

请注意，`function` 是一个模板，因此您可以定义类型 `function<T>` 的变量，并将可调用对象赋值给这些变量。例如：

```cpp
int f1(double);
function<int(double)> fct {f1};     // 初始化为 f1
int x = fct(2.3);                   // 调用 f1(2.3)
function<int(double)> fun;          // fun 可以保存任何 int(double)
fun = f1;
```

## B.6.3 pair 和 tuple

在 `<utility>` 中，标准库提供了一些“实用组件”，包括 `pair`：

```cpp
template <typename T1, typename T2>  
struct pair {
  using first_type = T1;
  using second_type = T2;
  T1 first;
  T2 second;

    // ... 拷贝和移动操作 ...
};

template <typename T1, typename T2>
constexpr pair<T1,T2> make_pair(T1 x, T2 y) { return pair<T1,T2>{x,y}; }
```

`make_pair()` 函数使使用 pair 变得简单。例如，下面是一个返回值和错误指示器的函数大纲：

```cpp
pair<double, error_indicator> my_fct(double d)
{
  errno = 0;      // 清除 C 风格全局错误指示器
  // ... 进行大量涉及 d 并计算 x 的运算 ...
  error_indicator ee = errno;
  errno = 0;      // 清除 C 风格全局错误指示器
  return make_pair(x, ee);
}
```

这个有用的习语示例可以这样使用：

```cpp
pair<int, error_indicator> res = my_fct(123.456);
if (res.second == 0) {
    // ... 使用 res.first ...
}
else {
    // 糟糕：出错
}
```

