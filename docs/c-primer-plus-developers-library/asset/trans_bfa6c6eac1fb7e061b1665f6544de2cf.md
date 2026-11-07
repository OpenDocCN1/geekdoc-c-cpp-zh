
```cpp
int main()
{
    using std::list;
    using std::cout;
    using std::endl;

    TooBig<int> f100(100); // limit = 100
    int vals[10] = {50, 100, 90, 180, 60, 210, 415, 88, 188, 201};
    list<int> yadayada(vals, vals + 10); // range constructor
    list<int> etcetera(vals, vals + 10);

    // C++11 can use the following instead
    // list<int> yadayada = {50, 100, 90, 180, 60, 210, 415, 88, 188, 201};
    // list<int> etcetera = {50, 100, 90, 180, 60, 210, 415, 88, 188, 201};

    cout << "Original lists:\n";
    for_each(yadayada.begin(), yadayada.end(), outint);
    cout << endl;
    for_each(etcetera.begin(), etcetera.end(), outint);
    cout << endl;

    yadayada.remove_if(f100);                    // use a named function object
    etcetera.remove_if(TooBig<int>(200));        // construct a function object

    cout << "Trimmed lists:\n";
    for_each(yadayada.begin(), yadayada.end(), outint);
    cout << endl;
    for_each(etcetera.begin(), etcetera.end(), outint);
    cout << endl;

    return 0;
}
```

一个仿函数（`f100`）是已声明的对象，第二个（`TooBig<int>(200)`）是通过构造函数调用创建的匿名对象。下面是程序清单16.15中程序的输出：

```text
Original lists:
50 100 90 180 60 210 415 88 188 201
50 100 90 180 60 210 415 88 188 201
Trimmed lists:
50 100 90 60 88
50 100 90 180 60 88 188
```

假设你已经有一个接受两个参数的模板函数：

```cpp
template <class T>
bool tooBig(const T& val, const T& lim)
{
    return val > lim;
}
```

可以用一个类将其转换为接受一个参数的函数对象：

```cpp
template<class T>
class TooBig2
{
private:
    T cutoff;

public:
    TooBig2(const T& t) : cutoff(t) {}

    bool operator()(const T& v)
    {
        return tooBig<T>(v, cutoff);
    }
};
```

也就是说，可以使用以下代码：

```cpp
TooBig2<int> tB100(100);
int x;
cin >> x;

if (tB100(x))       // same as if (tooBig(x, 100))
    ...
```

因此，调用 `tB100(x)` 与 `tooBig(x, 100)` 相同，但这个二元函数被转换为接受一个参数的函数对象，其中第二个参数用于构造该函数对象。简而言之，类仿函数 `TooBig2` 是一个函数适配器，它调整函数以满足不同的接口。

如清单中所述，C++11 的初始化列表特性简化了初始化。可以将

```cpp
int vals[10] = {50, 100, 90, 180, 60, 210, 415, 88, 188, 201};
list<int> yadayada(vals, vals + 10); // range constructor
list<int> etcetera(vals, vals + 10);
```

替换为：

```cpp
list<int> yadayada = {50, 100, 90, 180, 60, 210, 415, 88, 188, 201};
list<int> etcetera{50, 100, 90, 180, 60, 210, 415, 88, 188, 201};
```

## 预定义仿函数

STL 定义了几个基本仿函数。它们执行诸如将两个值相加、比较两个值是否相等等操作。提供它们是为了帮助支持那些以函数为参数的 STL 函数。例如，考虑 `transform()` 函数。它有两个版本。第一个版本接受四个参数。前两个参数是指定容器中范围的迭代器。（到目前，你一定已经熟悉这种方法。）第三个是指定将结果复制到何处的迭代器。最后一个参数是一个仿函数，它被应用于范围中的每个元素，以生成结果中的每个新元素。例如，考虑以下代码：

```cpp
const int LIM = 5;
double arr1[LIM] = {36, 39, 42, 45, 48};
```

```cpp
vector<double> gr8(arr1, arr1 + LIM);
ostream_iterator<double> out(cout, " ");
transform(gr8.begin(), gr8.end(), out, sqrt);
```

该代码计算每个元素的平方根，并将结果值发送到输出流。目标迭代器可以位于原范围内。例如，将本例中的 `out` 替换为 `gr8.begin()` 会用新值覆盖旧值。显然，所使用的仿函数必须能处理单个参数。

第二个版本使用接受两个参数的函数，将该函数应用于两个范围中各取一个元素。它多接受一个参数，该参数按顺序排在第三个，用于标识第二个范围的起始位置。例如，如果 `m8` 是第二个 `vector<double>` 对象，并且 `mean(double, double)` 返回两个值的均值，那么以下代码会输出 `gr8` 和 `m8` 中每对值的平均值：

```cpp
transform(gr8.begin(), gr8.end(), m8.begin(), out, mean);
```

现在假设你想将两个数组相加。不能将 `+` 用作参数，因为对于 `double` 类型，`+` 是内置运算符，而不是函数。你可以定义一个函数来相加两个数并使用它：

```cpp
double add(double x, double y) { return x + y; }
...
transform(gr8.begin(), gr8.end(), m8.begin(), out, add);
```

但那样就必须为每种类型分别定义一个函数。更好的做法是定义一个模板，不过你不必这样做，因为 STL 已经提供了。`functional`（原 `function.h`）头文件定义了几个模板类函数对象，其中包括一个名为 `plus<>` 的。

使用 `plus<>` 类进行普通加法是可行的，尽管有点别扭：

```cpp
#include <functional>
...
plus<double> add;    // create a plus<double> object
double y = add(2.2, 3.4); // using plus<double>::operator()
```

但它使提供函数对象作为参数变得容易：

```cpp
transform(gr8.begin(), gr8.end(), m8.begin(), out, plus<double>());
```

这里，代码没有创建具名对象，而是使用 `plus<double>` 构造函数构造一个仿函数来完成加法。（括号表示默认构造函数；传递给 `transform()` 的是构造出的函数对象。）

STL 为所有内置算术、关系和逻辑运算符提供了函数等价物。表16.12 列出了这些仿函数等价物的名称。它们可用于 C++ 内置类型，或任何重载了相应运算符的用户定义类型。

## 表16.12 运算符与仿函数等价物

| 运算符 | 仿函数等价物 |
|---|---|
| `+` | `plus` |
| `-` | `minus` |
| `*` | `multiplies` |
| `/` | `divides` |
| `%` | `modulus` |
| `-` | `negate` |
| `==` | `equal_to` |
| `!=` | `not_equal_to` |
| `>` | `greater` |
| `<` | `less` |
| `>=` | `greater_equal` |
| `<=` | `less_equal` |
| `&&` | `logical_and` |
| `\|\|` | `logical_or` |
| `!` | `logical_not` |

## 注意

较旧的 C++ 实现使用仿函数名 `times` 而不是 `multiplies`。

### 可适配仿函数与函数适配器

表16.12 中的预定义仿函数都是*可适配的*。实际上，STL 有五个相关概念：可适配生成器、可适配一元函数、可适配二元函数、可适配谓词和可适配二元谓词。

仿函数之所以可适配，是因为它带有标识其参数类型和返回类型的 `typedef` 成员。这些成员分别称为 `result_type`、`first_argument_type` 和 `second_argument_type`，其含义与名称相符。例如，`plus<int>` 对象的返回类型标识为 `plus<int>::result_type`，而它会是 `int` 的 `typedef`。

仿函数可适配的意义在于，它随后可以被函数适配器对象使用，而这些对象假定这些 `typedef` 成员存在。例如，一个函数的参数若是可适配仿函数，该函数可以使用 `result_type` 成员声明一个与其返回类型匹配的变量。

事实上，STL 提供了使用这些机制的函数适配器类。例如，假设你想将向量 `gr8` 的每个元素乘以 2.5。这需要使用带一元函数参数的 `transform()` 版本，就像前面示例所示：

```cpp
transform(gr8.begin(), gr8.end(), out, sqrt);
```

`multiplies()` 仿函数可以完成乘法，但它是二元函数。因此需要一个函数适配器，把接受两个参数的仿函数转换为接受一个参数的仿函数。前面的 `TooBig2` 示例展示了一种方式，但 STL 通过 `binder1st` 和 `binder2nd` 类自动化了这一过程，它们将可适配二元函数转换为可适配一元函数。

来看 `binder1st`。假设你有一个可适配二元函数对象 `f2()`。可以创建一个 `binder1st` 对象，将名为 `val` 的特定值绑定为 `f2()` 的第一个参数：

```cpp
binder1st(f2, val) f1;
```

然后，用其单个参数调用 `f1(x)` 返回的值，与以 `val` 为第一个参数、以 `f1()` 的参数为第二个参数调用 `f2()` 返回的值相同。也就是说，`f1(x)` 等价于 `f2(val, x)`，只不过它是一元函数而不是二元函数。`f2()` 函数已被适配。同样，只有当 `f2()` 是可适配函数时，这才可能。

这可能看起来有点别扭。不过，STL 提供了 `bind1st()` 函数来简化 `binder1st` 类的使用。你向它提供函数名和用于构造 `binder1st` 对象的值，它返回该类型的对象。例如，可以将二元函数 `multiplies()` 转换为将其参数乘以 2.5 的一元函数。只需这样做：

```cpp
bind1st(multiplies<double>(), 2.5)
```

因此，将 `gr8` 中每个元素乘以 2.5 并显示结果的解决方案如下：

```cpp
transform(gr8.begin(), gr8.end(), out,
     bind1st(multiplies<double>(), 2.5));
```

`binder2nd` 类类似，只是它将常量赋给第二个参数而不是第一个参数。它有一个名为 `bind2nd` 的辅助函数，其工作方式与 `bind1st` 类似。

