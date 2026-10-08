

```cpp
cout << '<<';
```

对于 filter_view 也是如此：

点击此处查看代码图像

```cpp
for (int x : filter_view{ r, [](int x) { return x % 2; } }, 3 })
cout << '<<';
```

这些视图（views）可能会迅速变得复杂，因此有一种替代方案：管道（pipelines §14.4）。标准库提供了许多视图，它们也可以作为范围适配器：

| 标准库视图（范围适配器）<ranges> | v 是视图；r 是范围；p 是谓词；n 是整数 |
| all_view(r) | v 是来自 r 的所有元素 |
| filter_view(r,p) | v 是 r 中满足 p 的元素 |
| transform_view(r,f) | v 是对 r 中每个元素调用 f 的结果 |
| take_view(r,n) | v 是 r 中至多 n 个元素 |
| take_while(r,p) | v 是 r 中的元素，直到某个元素不再满足 p 为止 |
| drop_view(r) | v 是从第 n+1 个元素开始的 r 中的元素 |
| drop_while(r,p) | v 是从第一个满足 p 的元素开始的 r 中的元素 |
| join_view(r) | v 是 r 的扁平化版本；r 的元素必须是范围 |
| split_view(r,d) | v 是由分隔符 d 确定的子范围范围；d 是元素或范围 |
| common_view(r) | 由 (begin, end) 元组描述 |
| reverse_view(r) | v 是 r 的反序元素；r 必须具有双向访问能力 |
| views::elements<>(r) | v 是 r 中元组元素中第 n 个元素的范围 |
| keys_view(r) | v 是 r 中成对元素中第一个元素的范围 |
| values_view(r) | v 是 r 中成对元素中第二个元素的范围 |
| ref_view(r) | v 是指向 r 中元素引用的范围 |

视图提供了一个与范围（range）非常相似的接口，因此在许多情况下，我们可以在任何地方相同地使用视图。关键区别在于视图不拥有其元素；它不负责其底层范围的元素——那是范围的责任。另一方面，视图的生存时间不能超过它的范围：

点击此处查看代码图像

```cpp
auto bad() {
  vector v = {1, 2, 3, 4};
  return filter_view(v,odd);
}
// v 在视图之前就会被销毁
```

视图get应该是廉价拷贝的，因此请按值传递它们。我使用了标准类型来保持示例简单，但当然，我们可以为自己的自定义类型创建视图。例如：

点击此处查看代码图像

```cpp
struct Reading {
    int location();
    int temperature();
    int humidity();
    int air_pressure();
    //...
}
int average_temp(vector<Reading> readings) {
    if (readings.size()==0) throw No_readings();
    double s = 0;
    for (int x : views::elements<1>(readings))
        s += x;
    return s/readings.size();
}
```

## 14.3 生成器

通常，范围需要动态生成。标准库为此提供了一些简单的生成器（又称工厂）：

| 范围工厂 <ranges> | v 是视图；x 是元素类型 T 的元素；is 是 istream |
| v=empty_view<T>() | v 是类型 T 的空范围（如果有的话） |
| v=single_view(x) | v 是一个包含单个元素 x 的范围 |
| v=iota_view(x) | v 是无限元素范围：x, x+1, x+2, ... 使用 ++ 进行递增 |
| v=iota_view(x,y) | v 是包含 n 个元素的范围：x, x+1, ..., y-1 使用 ++ 进行递增 |
| v=istream_view<T>(is) | v 是通过对 is 调用 >> 到 T 获取的范围 |

Iota 视图用于生成简单的序列非常有用。例如：

点击此处查看代码图像

```cpp
for (int x : iota_view<int>(42)) 
  cout << x;
```

istream_view 提供了一个在范围循环中使用 istream 的简单示例：

点击此处查看代码图像

```cpp
for (auto x : istream_view<double>(cin))
  cout << x;
```

和其他视图一样，istream_view 可以与其他视图组合在一起：

点击此处查看代码图像

```cpp
auto cpx = istream_view<double>(cin);
for (auto x : transform_view(cpx, [](auto z){ return z; }))
  cout << x;
```

## 14.4 管道

对于每个标准视图，标准库都提供一个产生过滤器的函数；即一个可以作为过滤器适配器参数的对象。例如，filter_view 允许按序列组合过滤器，而不是将它们作为一组嵌套调用的形式呈现。管道样式（使用管道适配器）被认为比嵌套调用更具可读性。管道从左到右工作；即 f 的结果传递给 g，因此初始 r 必须是一个范围或生成器。这些过滤函数位于 views::views 命名空间中：

```cpp
void user(forward_range auto r)
{
  auto odd = [](int x) { return x % 2; };
  for (int x : r | views::filter(odd) | views::take(3))
    cout << x;
}
```

视图和管道的实现涉及一些令人头疼的元编程，如果你担心性能，请确保测量你的实现是否提供了你所需。如果不是，总有一种传统的变通方法：

点击此处查看代码图像

```cpp
void user(forward_range auto r)
{
  int count = 0;
  for (int x : r) {
    cout << x;
    if (++count == 3) return;
  }
}
```

然而，其运行逻辑被模糊了。

## 14.5 概念概述

标准库提供了许多实用的概念：

- 定义类型属性的概念（§14.5.1）
- 定义迭代器的概念（§14.5.2）
- 定义范围的概念（§14.5.3）

### 14.5.1 类型概念

概念涉及类型的属性，并且它们之间的关系反映了类型的多样性。这些概念有助于简化模板。

| 核心语言概念 <concepts> | T 和 U 是类型 |
| same_as<T,U> | T 与 U 相同 |
| derived_from<T,U> | T 继承自 U |
| convertible_to<T,U> |一个 T 可以转换为 U |
| common_reference_with<T,U> | T 和 U 共享一个共同引用类型 |
| common_with<T,U> | T 和 U 共享一个共同类型 |
| integral<T> | T 是整数类型 |
| signed_integral<T> | T 是有符号整数类型 |
| unsigned_integral<T> | T 是无符号整数类型 |
| floating_point<T> | T 是浮点类型 |
| assignable_from<T,U> | 一个 U 可以赋值给 T |
| swappable<T,U> | 一个 T 可以与 U 交换 |
| swappable_with<T,T> | |

许多算法与相关类型的组合工作，例如混合了整数和浮点数的表达式。我们使用 common_with 来说明这种混合在数学上是合理的。如果 common_with<X,Y> 为真，我们使用 common_type_t<X,Y> 通过首先转换为 common_type_t<X,Y> 来比较 X 和 Y。例如：

点击此处查看代码图像

```cpp
common_type<string, const char> s1 = some_fct();
common_type<string, const char> s2 = some_other_fct();
```

```cpp
if (s1<s2) {
  ...
}
```

为了为一对类型指定共同类型，我们特化在 common 定义中使用的 common_type_t。例如：

点击此处查看代码图像

```cpp
using common_type_t<Bigint,long> = Bigint; // 适用于合适的 Bigint 定义
```

