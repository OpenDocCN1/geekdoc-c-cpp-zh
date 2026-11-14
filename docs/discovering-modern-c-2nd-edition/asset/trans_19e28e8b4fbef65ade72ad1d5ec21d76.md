

```
private:
Range& r; // requires lvalue!
};
```

它只是持有范围的引用，并提供 `begin` 和 `end` 迭代器。`end` 迭代器中的位置不会被使用，并被设置为任意值。即使迭代器也可以以简单的方式实现：

Click here to view code image

```
template <typename Range>
class enumerate_iterator
{
    using riter = decltype(std::begin(std::declval<Range>()));
    using self = enumerate_iterator<Range>;

public:
    explicit enumerate_iterator(int index, riter it) :
    index(index), it(it) {}

    auto operator*() const noexcept { return make_pair(index, *it); }
    bool operator!=(self other) const noexcept { return it != other.it; }
    self& operator++() noexcept { ++index; ++it; return *this; }

private:
    int index;
    riter it;
};
```

如你所见，我们只比较底层迭代器，并在比较中忽略索引。解引用运算符返回索引和范围迭代器的一对。我们现在可以在基于范围的 `for` 循环中使用我们的视图来枚举 `vector` 的条目：

Click here to view code image

```
vector<int> seq = {3, 4, 7, 9, 2, 5, 7, 8, 3, 4, 3, 9};
for (auto [i, value] : enumerate_view(seq))
cout << "The " << i << "th value is " << value << endl;
```

为了与标准视图保持一致，我们还提供相应的适配器，它可以像函数一样调用：

```cpp
namespace views {
struct enumerate_t
{
    template <typename Range>
    enumerate_view<Range> operator()(Range&& r) const noexcept
    {
        return enumerate_view<Range>{std::forward<Range>(r)};
    };
    static constexpr enumerate_t enumerate;
}
for (auto [i, value] : views::enumerate(seq))
cout << "The " << i << "th value is " << value << endl;
```

当然，我们也希望为我们的视图提供管道运算符：

```cpp
namespace views {
template <typename Range>
enumerate_view<Range> operator|(Range&& r, enumerate_t) noexcept
{
    return enumerate_view<Range>{std::forward<Range>(r)};
}
for (auto [i, value] : seq | views::enumerate)
cout << "The " << i << "th value is " << value << endl;
```

这个功能齐全的生产代码将包含更多细节，例如更丰富的迭代器接口及其行为的一些类型声明，但我们的极简实现中已经提供了基本行为。在意识到这有多简单之后，作者后悔没有早点这样做。话虽如此，我们邀请你在有帮助时实现自己的范围。如前所述，迭代器是最大化适用性的绝妙主意，但它不应该是应用程序级别工作的主要接口。

## C++17 4.1.6 并行计算

在 C++17 中，大多数 STL 算法都可以并行执行。相应的函数被重载为新的实现，以执行策略开头，后跟我们熟悉的函数参数。所有策略都位于命名空间 std::execution 中。要顺序执行算法（与以前一样，我们可以使用策略 seq 或完全省略它。因此，以下两个调用是等价的：

```
sort(seq, begin(v), end(v));
sort(begin(v), end(v));
```

### 策略 par:

```
sort(par, begin(v), end(v));
```

触发多线程执行，而每个线程中的计算是顺序的。为了发挥硬件的最大潜力，我们可以使用 par_unseq：

```
sort(par_unseq, begin(v), end(v));
```

它还允许在每个线程内并行（即非顺序地）执行操作。在实践中，这通常意味着数值操作使用 SSE/AVX 加速。

![](img/5682e787fc967e93d7e33e8bac5f58a0_372_0.png)

在 C++20 中添加了策略 unseq，用于在单个线程上非顺序计算。为了测试并行排序，我们在四核 Intel Core i7-8550U（1.8 GHz）上的 Visual Studio 2019 版本 16.9.3 中进行了测试，对 1000 万个 int 值进行排序时得到了以下墙钟时间：

Click here to view code image

```
Sorting with seq took 0.82638s.
Sorting with par took 0.216368s.
Sorting with unseq took 0.819744s.
Sorting with par_unseq took 0.219476s.
```

我们可以看到，多线程版本大约快四倍，而线程内的并行化并没有加速执行，因为 SSE/AVX 对排序 int 值帮助不大。然而，本书的一位审稿人在他的机器上观察到 unseq 的结果最快。在其他编译器上，我们没有看到并行策略的好处（系统也没有指示使用多个线程）。因此，在你喜欢的平台上尝试绝对值得。

在并行化的背景下，添加了七个新算法：

- `for_each_n` 将函子应用于前 `n` 个条目；
- `reduce` 执行类似于 `accumulate` 的归约，但允许顺序改变；
- `transform_reduce` 在归约前应用函子（通常称为 map-reduce）；
- `inclusive_scan` 计算类似于现有顺序函数 `partial_sum` 的部分和；
- `exclusive_scan` 也计算部分和，其中第 i 个条目被排除在第 i 个部分和之外；以及
- `transform_inclusive_scan` 和 `transform_exclusive_scan` 在对每个条目应用函子后计算相应的部分和。

```
=> c++20/parallel_reduce.cpp
```

我们希望 `reduce` 操作可以受益于 AVX 加速。对于十亿个 `double` 值的大型集合，我们在前面提到的 i7 上进行了测量：

Click here to view code image

```
Reducing with seq     took 0.429475s.
Reducing with par     took 0.2653s.
Reducing with unseq   took 0.42294s.
Reducing with par_unseq took 0.261549s.
```

在此计算中，限制因素显然是内存带宽，我们将这种加速归功于第二个内存通道，它使多线程能够更快地加载。为了摆脱带宽限制，我们测量了较小的集合，其中由于线程管理开销，顺序版本甚至比并行版本更快。而且，我们仍然看不到 `par_unseq` 策略相对于 `par` 的好处。

最后的评论：本节仅浅尝辄止地介绍了 STL，旨在作为开胃小菜。

## 4.2 数值计算

在本节中，我们将说明如何使用 C++ 的复数和随机数生成器。头文件 <cmath> 包含大量数值函数，其用法简单直接，无需进一步说明。

### 4.2.1 复数

我们已经在第 2 章中演示了如何实现非模板复数类，并在第 3 章中使用了复数类模板。为了不一遍又一遍地重复显而易见的内容，我们用图形示例来说明用法。

#### 4.2.1.1 曼德布罗特集

曼德布罗特集——以其创建者 Benoit B. Mandelbrot 命名——是通过连续平方并添加原始值而不会趋于无穷大的复数集合：

```
$$M = \left\{ c \in \mathbb{C} : \lim_{n \to \infty} z_n(c) \neq \infty \right\}$$
```

其中

```
$$z_0(c) = c$$ $$z_{n+1}(c) = z_n^2 + c$$
```

可以证明，当 $|z_n(c)| > 2$ 时，一点在曼德布罗特集之外。计算模长最耗费资源的部分是最后的平方根。C++ 提供了一个函数 `norm`，它是 `abs` 的平方，即计算 `abs` 而不进行最后的 `sqrt`。因此，我们将继续标准 `abs(z) <= 2` 替换为 `norm(z) <= 4`。

曼德布罗特集的可视化是达到该极限所需迭代次数的颜色编码。为了绘制分形，我们使用了跨平台库 Simple DirectMedia Layer (SDL 1.2)。数值部分由类 `mandel_pixel` 实现，它为每个像素计算直到 `norm(z) > 4` 所需的迭代次数以及代表该迭代次数的颜色：

Click here to view code image

```
class mandel_pixel
{
public:
	mandel_pixel(SDL_Surface* screen, int x, int y,
		int xdim, int ydim, int max_iter)
		: screen(screen), max_iter(max_iter), iter(0), c(x, y)
	{
		// scale y to [-1.2,1.2] and shift -0.5+0i to the
		center
		c *= 2.4f / static_cast<float>(ydim);
		c -= complex<float>(1.2 * xdim / ydim + 0.5, 1.2);
		iterate();
	}
	int iterations() const { return iter; }
	uint32_t color() const { ... }

private:
	void iterate()
	{
		complex<float> z = c;
		for (; iter < max_iter && norm(z) <= 4.0f; iter++)
			z = z * z + c;
	};
	// ...

	int iter;
	complex<float> c;
};
```

复数被缩放，使得对于任何图像大小，它们的虚部都介于 -1.2 和 1.2 之间。然后将图像向左移动 0.5。我们省略了图形的代码行，因为我们想在这里专注于复数。完整的程序可以在 GitHub 上找到，生成的图片见图 4-7。

