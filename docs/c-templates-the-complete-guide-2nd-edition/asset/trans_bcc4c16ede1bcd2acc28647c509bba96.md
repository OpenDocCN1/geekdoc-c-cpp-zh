

足以满足 C++98 标准。语言中引入了作用域枚举类型，而它们没有这种隐式转换，这使得枚举类型的检测变得复杂。
31 如果一个拷贝或移动构造函数在效果上可以被底层字节的简单拷贝所替代，则称其为 *trivial*。

```
{
T tmp(x);
x = y;
y = tmp;
}
```

该实现涉及三次拷贝操作。然而，对于某些类型，我们可以提供更高效的 swap() 操作，例如对于 Array<T>，它将数据存储为指向数组内容的指针和长度：
Click here to view code image

```
template<typename T>
void swap(Array<T>& x, Array<T>& y)
{
swap(x.ptr, y.ptr);
swap(x.len, y.len);
}
```

两种 swap() 实现都会正确交换两个 Array<T> 对象的 contents。然而，后一种实现更高效，因为它利用了 Array<T> 的额外属性（具体来说是对 ptr 和 len 及其各自作用的了解），而这些属性对于任意类型来说是不可用的。¹ 因此，后一种函数模板在概念上比前一种更专业，因为它对前一种函数模板接受的类型子集执行相同的操作。幸运的是，基于函数模板的部分排序规则（参见第 16.2.2 节第 330 页），第二个函数模板也是更专业的，因此编译器在适用时（即对于 Array<T> 参数）会选择更专业（因此更高效）的函数模板，并在更专业的版本不适用时回退到更通用（可能效率较低）的算法。

引入通用算法的更专业变体的设计和优化方法称为算法专业化。更专业的变体适用于通用算法的有效输入的子集，基于类型或类型的特定属性来识别该子集，并且通常比该通用算法的最通用实现更高效。

算法专业化的实现至关重要的一点是，更专业的变体在适用时会被自动选择，而调用者无需意识到这些变体的存在。在我们的 swap() 示例中，这是通过重载（概念上）更专业的函数模板（第二个 swap()）与最通用的函数模板（第一个 swap()）来实现的，并确保更专业的函数模板根据 C++ 的部分排序规则也是更专业的。

并非所有概念上更专业的算法变体都可以直接转换为提供正确部分排序行为的函数模板。对于我们的下一个示例，请考虑 However, the alternative presented here is more broadly applicable.

advanceIter() 函数（类似于 C++ 标准库中的 std::advance()），它将迭代器 x 向前移动 n 步。该通用算法可以操作任何输入迭代器： Click here to view code image

```
template<typename InputIterator, typename Distance>
void advanceIter(InputIterator& x, Distance n)
{
while (n > 0) { //linear time
++x;
--n;
}
}
```

对于一类迭代器——提供随机访问操作的迭代器——我们可以提供更高效的实现： Click here to view code image

```
template<typename RandomAccessIterator, typename Distance>
void advanceIter(RandomAccessIterator& x, Distance n) {
 x += n; // constant time
}
```

不幸的是，同时定义这两个函数模板会导致编译器错误，因为——正如介绍中所述——仅基于模板参数名称不同的函数模板是不可重载的。本章的其余部分将讨论模拟重载这些函数模板所需效果的技术。

## 20.2 Tag Dispatching

算法专业化的一种方法是使用唯一的类型为算法的不同实现变体“标记”，该类型标识该变体。例如，为了解决刚刚介绍的 advanceIter() 问题，我们可以使用标准库的迭代器类别标记类型（定义如下）来标识 advanceIter() 算法的两个实现变体： Click here

```
```cpp
template<typename Iterator, typename Distance>
void advanceIterImpl(Iterator& x, Distance n,
std::input_iterator_tag)
{
while (n > 0) { //linear time
++x;
--n;
}
}

template<typename Iterator, typename Distance>
void advanceIterImpl(Iterator& x, Distance n,
std::random_access_iterator_tag) {
x += n; // constant time
}
```
```

然后，`advanceIter()` 函数模板本身只需连同适当的标记一起转发其参数：

```
```cpp
template<typename Iterator, typename Distance>
void advanceIter(Iterator& x, Distance n)
{
advanceIterImpl(x, n,
typename
std::iterator_traits<Iterator>::iterator_category());
}
```
```

特征类 `std::iterator_traits` 通过其成员类型 `iterator_category` 为迭代器提供类别。迭代器类别是前面提到的 _tag types 之一，它指定该类型是什么样的迭代器。在 C++ 标准库内部，可用的标记定义如下，使用继承来反映一个标记描述的类别是从另一个类别派生而来时：

```
```cpp
namespace std {
struct input_iterator_tag {};
struct output_iterator_tag {};
struct forward_iterator_tag : public input_iterator_tag { };
struct bidirectional_iterator_tag : public forward_iterator_tag { };
struct random_access_iterator_tag : public bidirectional_iterator_tag
{ };
}
```
```

有效使用标记分派的关键在于标记之间的关系。我们的两个 `advanceIterImpl()` 变体分别用 `std::input_iterator_tag` 和 `std::random_access_iterator_tag` 标记，并且由于

std::random_access_iterator_tag 继承自 std::input_iterator_tag，普通的函数重载将在使用随机访问迭代器调用 advanceIterImpl() 时优先选择更专业的算法变体（使用 std::random_access_iterator_tag）。因此，标记分派依赖于从单个主函数模板委托到一组 _impl 变体，这些变体被标记为使得普通的函数重载会选择最适合给定模板参数的最专业算法。

当算法使用的属性具有自然的层次结构并且存在提供这些标记值的现有特征集时，标记分派效果很好。当算法专业化依赖于特设的类型属性时，例如类型 T 是否具有平凡的拷贝赋值运算符，则就不那么方便了。对于这种情况，我们需要一种更强大的技术。

## 20.3 Enabling/Disabling Function Templates

算法专业化涉及提供不同的函数模板，这些模板基于模板参数的属性进行选择。不幸的是，函数模板的部分排序（第 16.2.2 节第 330 页）或重载解析（附录 C）都不足以表达更高级形式的算法专业化。

C++ 标准库为此提供的一个助手是 std::enable_if，它在第 6.3 节第 98 页中介绍。本节讨论如何通过引入相应的别名模板来实现该助手，我们将其称为 EnableIf 以避免名称冲突。

就像 std::enable_if 一样，EnableIf 别名模板可用于在特定条件下启用（或禁用）特定的函数模板。例如，advanceIter() 算法的随机访问版本可以实现如下： [Click here to view code image](#)

```
template<typename Iterator>
constexpr bool IsRandomAccessIterator =
  IsConvertible<
    typename std::iterator_traits<Iterator>::iterator_category,
    std::random_access_iterator_tag>;
template<typename Iterator, typename Distance>
EnableIf<IsRandomAccessIterator<Iterator>>
advanceIter(Iterator& x, Distance n){
  x += n; // constant time
```

