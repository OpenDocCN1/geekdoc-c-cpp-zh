

当我们遍历容器时，得到的是键及其关联值的对（因为单独的值本身是没有意义的）。

```
=> c++11/multimap.test.cpp
```

当一个键可以关联多个值时，我们需要 multimap。相同键的条目被存储在彼此相邻的位置，因此我们可以遍历它们。迭代器范围由 lower_bound 和 upper_bound 方法提供。在下一个示例中，我们遍历所有键等于 3 的条目并打印它们的值：

```
multimap<int, double> mm=
{{3, 1.3}, {2, 4.1}, {3, 1.8}, {4, 9.2}, {3, 1.5}};
for (auto it = mm.lower_bound(3),
    end = mm.upper_bound(3); it != end; ++it)
    cout << "The value is " << it->second << '\n';
```

这将产生：

The value is 1.3
The value is 1.8
The value is 1.5

最后四个容器——set、multiset、map 和 multimap——都以某种树的形式实现，访问的复杂度为对数复杂度。在下一节中，我们介绍平均复杂度下访问更快的容器。

## 4.1.3.6 哈希表

```
=> c++11/unordered_map.test.cpp
```

哈希表是具有非常高效搜索能力的容器。与前面的容器不同，哈希映射在单次访问时具有常数复杂度（前提是哈希函数足够好）。为了避免与现有软件发生名称冲突，标准委员会避免使用带有“hash”的名称，并在有序容器的名称前加上了“unordered”。

无序容器的使用方式与其有序对应物相同：

```
unordered_map<string, double> constants=
{{"e", 2.7}, {"pi", 3.14}, {"h", 6.6e-34}};
cout << "The Planck constant is " << constants["h"] << '\n';
constants["c"] = 299792458;
cout << "The Euler constant is " << constants.at("e") << "\n\n";
```

这与 map 产生相同的结果。如果需要，可以提供用户定义的哈希函数。

**进一步阅读：** 所有容器都提供可自定义的分配器，允许我们实现自己的内存管理或使用平台特定的内存。分配器接口例如在 [26]、[43] 中给出。

## 4.1.4 算法

通用 STL 算法定义在头文件 <algorithm> 中，而主要用于数值计算的算法定义在 <numeric> 中。

### 4.1.4.1 不修改的序列操作

find 接受三个参数：两个定义搜索空间右开区间的迭代器，以及在该范围内要搜索的值。每个由 first 引用的条目都与 value 进行比较。当找到匹配项时，返回指向它的迭代器；否则递增迭代器。如果值不在序列中，则返回等于 last 的迭代器。因此，调用者可以通过将结果与 last 进行比较来测试搜索是否成功。

这实际上并不是一项特别困难的任务，我们可以自己实现：

```
template <typename InputIterator, typename T>
InputIterator find(InputIterator first, InputIterator last,
                   const T& value)
{
    while (first != last && *first != value)
        ++first;
    return first;
}
```

这段代码片段确实是 find 的标准实现方式，尽管针对特殊迭代器可能存在专用重载。

=> c++11/find_test.cpp

作为演示，我们考虑一个包含两次数字 7 的整数序列。我们想要编写一个以第一个 7 开始、以第二个 7 结束的子序列。换句话说，我们必须找到这两个出现位置并打印出一个闭区间——而 STL 始终使用右开区间。这需要一些额外的工作：

```
vector<int> seq = { 3, 4, 7, 9, 2, 5, 7, 8};
auto it = find(seq.begin(), seq.end(), 7); // first 7
auto end = find(it+1, seq.end(), 7); // second 7
for (auto past = end+1; it != past; ++it)
    cout << *it << ' ';
cout << '\n';
```

在找到第一个 7 之后，我们从下一个位置重新开始搜索（以免再次找到同一个 7）。在 for 循环中，我们递增结束迭代器，以免在打印中包含第二个 7。在上面的示例中，我们依赖于 7 在序列中出现两次这一事实。为了健壮性，当 7 未找到或只找到一次时，我们抛出用户定义的异常。

为了更健壮，我们可以检查搜索是否成功：

```
if (it == seq.end())
    throw no_seven();
...
if (end == seq.end())
    throw one_seven{};
```

上面的实现不适用于 list，因为我们使用了 it+1 和 end-1 这样的表达式。这要求迭代器是随机访问迭代器。然而，我们可以通过复制一个迭代器并使用递增操作来消除这一要求：

```cpp
list<int> seq = {3, 4, 7, 9, 2, 5, 7, 8};
auto it = find(seq.begin(), seq.end(), 7), it2 = it; // first 7
++it2;
auto end = find(it2, seq.end(), 7); // second 7
++end;
for (; it != end; ++it)
    std::cout << *it << ' ';
```

这种迭代器用法与前面的实现差别不大，但通过避免随机访问操作，它更具通用性。例如，我们现在可以使用 list。更正式地说：我们的第二个实现只要求 it 和 end 为前向迭代器，而第一个实现需要随机访问迭代器。

采用同样的风格，我们可以编写一个适用于所有 STL 容器的通用函数来打印区间。让我们更进一步：我们还想支持经典数组。不幸的是，数组没有 begin() 和 end() 成员。（没错，它们根本没有成员。）C++11 为它们和所有 STL 容器提供了名为 begin() 和 end() 的自由函数，这使我们能够更具通用性：

### 列表 4-2：打印闭区间的通用函数

```cpp
struct value_not_found {};
struct value_not_found_twice {};

template <typename Range, typename Value>
void print_interval(const Range& r, const Value& v,
                    std::ostream& os = std::cout)
{
    using std::begin; using std::end;
    auto it = std::find(begin(r), end(r), v), it2 = it;
    if (it == end(r))
        throw value_not_found();
    ++it2;
    auto past = std::find(it2, end(r), v);
    if (past == end(r))
        throw value_not_found_twice();
    ++past;
    for (; it != past; ++it)
        os << *it << ' ';
}

int main ()
{
    std::list<int> seq = { 3, 4, 7, 9, 2, 5, 7, 8 };
    print_interval(seq, 7);

    int array[] = { 3, 4, 7, 9, 2, 5, 7, 8 };
    std::stringstream ss;
    print_interval(array, 7, ss);
    std::cout << ss.str();
}
```

我们还对输出流进行了参数化，以不局限于 std::cout。请注意函数参数中静态多态与动态多态的和谐混合：范围 r 和值 v 的类型在编译期间实例化，而 os 的输出运算符 << 在运行时根据 os 实际引用的类型进行选择。

此时，我们想向您说明我们处理命名空间的方式。当我们使用大量标准容器和算法时，可以在包含头文件后直接声明

```
using namespace std;
```

然后就不再需要编写 std:: 了。这对于小型程序来说没问题。但在大型项目中，迟早会遇到名称冲突。修复它们可能既费时又令人烦恼（在此，预防胜于治疗）。因此，我们应该尽可能少地导入命名空间——尤其是在头文件中。我们对 print_interval 的实现不依赖于先前的名称导入，可以安全地放置在头文件中。即使在函数内部，我们也不导入整个 std 命名空间，而是仅限于我们实际使用的函数。

请注意，我们在某些函数调用中没有限定命名空间，例如 std::begin(r)。这在上面的示例中可行，但我们无法覆盖在类的命名空间中定义 begin 函数的用户类型。using std::begin 和 begin(r) 的组合保证能找到 std::begin。另一方面，用户类型的 begin 函数通过 ADL（§3.2.2）查找到，并且会比 std::begin 更匹配。end 也是如此。相比之下，对于 find 函数，我们不想调用可能的用户重载，并确保它来自 std。

find_if 通过搜索满足一般条件的第一个条目来推广 find。它不再与单个值进行比较，而是评估一个 Predicate——一个返回 bool 的函数。假设我们要搜索第一个大于 4 且小于 7 的列表条目：

```
bool check(int i) { return i > 4 && i < 7; }
```

```
int main() {
    list<int> seq = { 3, 4, 7, 9, 2, 5, 7, 8 };
    auto it = find_if(begin(seq), end(seq), check);
    cout << "The first value in range is " << *it << '\n';
}
```

或者我们就地创建谓词：

```
auto it = find_if(begin(seq), end(seq),
[](int i){ return i > 4 && i < 7; });
```

