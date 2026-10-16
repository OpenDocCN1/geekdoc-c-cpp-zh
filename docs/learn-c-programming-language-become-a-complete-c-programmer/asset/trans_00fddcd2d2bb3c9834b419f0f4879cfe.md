

这对于一个简单的概念来说显得相当冗长。然而，我希望对所有运算符以及它们使用的对称性做出明确说明，而不是将复杂性隐藏在概括之中。

在此基础上，我们可以定义 find()：

```
template<typename Iter, typename Val>
Iter find(Iter b, Iter e, Val x)
{
static_assert(Input_iterator<Iter>(), "find() requires an input iterator");
static_assert(Equality_comparable<Value_type<Iter>,Val>(), "find()'s iterator and value arguments must match");
while (b!=e) {
if (*b==x) return b; ++b;
}
return b;
```

## Section 24.4.2 Multi-argument Concepts

多参数概念在指定通用算法时特别常见且有用。这也是你会发现概念数量最多、并且需要指定新概念的地方最多（而不是从常用概念的目录中挑选“标准”概念）。众所周知类型的变化似乎比算法对其参数的要求变化更有限。

## 24.4.3 Value Concepts

概念可以表达对一组模板参数的任意（语法）要求。特别是，模板参数可以是整数值，因此概念可以接受整数参数。例如，我们可以编写一个约束检查来测试值模板参数是否很小：

```
template<int N>
constexpr bool Small_size()
{
return N<=8;
}
```

一个更现实的例子是概念中数值参数只是其中之一。例如：

```
constexpr int stack_limit = 2048;
template<typename T,int N>
constexpr bool Stackable() // T is regular and N elements of T can fit on a small stack {
return Regular<T>() && sizeof(T)*N<=stack_limit;
```

这实现了“小到可以栈分配”的概念。它可能像这样使用：

```
template<typename T, int N>
struct Buffer {
//...
};
template<typename T, int N> void fct()
{
static_assert(Stackable<T,N>(),"fct() buffer won’t fit on stack");
Buffer<T,N> buf;
//...
}
```

与类型的<|message|>
Compared to the fundamental concepts for types, value concepts tend to be small and ad hoc.

## 24.4.4 Constraints Checks

本书中使用的约束检查可以在本书的支持网站上找到。它们不是标准的一部分，我希望将来它们会被适当的语言机制取代。然而，它们对于思考模板和类型设计很有用，并反映了标准库中 de facto 的概念。它们应放在单独的命名空间中，以避免干扰可能的未来语言特性和概念思想的替代实现。我使用命名空间 Estd，但那可能是一个别名（§14.4.2）。以下是你可能会觉得有用的几个约束检查：

- **Input_iterator<X>**: **X** 是一个迭代器，我们只能使用一次来遍历序列（使用 ++ 向前），每个元素只读取一次。
- **Output_iterator<X>**: **X** 是一个迭代器，我们只能使用一次来遍历序列（使用 ++ 向前），每个元素只写入一次。
- **Forward_iterator<X>**: **X** 是一个迭代器，我们可以使用它来遍历序列（使用 ++ 向前）。这就是单链表（例如 **forward_list**）自然支持的。
- **Bidirectional_iterator<X>**: **X** 是一个迭代器，我们可以向前（使用 ++）和向后（使用--）移动。这就是双向链表（例如 **list**）自然支持的。
- **Random_access_iterator<X>**: **X** 是一个迭代器，我们可以使用它来遍历序列（向前和向后）并使用下标随机访问元素，以及使用 += 和 -= 进行定位。这就是数组自然支持的。
- **Equality_comparable<X,Y>**: 一个 **X** 可以使用 == 和 != 与一个 **Y** 进行比较。
- **Totally_ordered<X,Y>**: **X** 和 **Y** 是 **Equality_comparable**，并且一个 **X** 可以使用 <, <=, > 和 >= 与一个 **Y** 进行比较。
- **Semiregular<X>**: **X** 可以被复制、默认构造、在自由存储上分配，并且没有烦人的次要技术限制。
- **Regular<X>**: Xs 是 **Semiregular** 并且可以使用相等进行比较。标准库容器要求其元素是 regular 的。
- **Ordered<X>**: Xs 是 **Regular** 和 **Totally_ordered.** 标准库关联容器要求其元素是有序的，除非你显式提供比较操作。
- **Assignable<X,Y>**: 一个 **Y** 可以使用 = 分配给一个 **X**。
- **Predicate<F,X>**: 一个 **F** 可以对一个 **X** 调用并产生一个 **bool**。
- **Streamable<X>**: 一个 **X** 可以使用 iostreams 进行读写。
- **Movable<X>**: 一个 **X** 可以被移动；也就是说，它具有移动构造函数和移动赋值。此外，一个 **X** 是可寻址的并且可析构的。
- **Copyable<X>**: 一个 **X** 是 **Movable** 并且也可以被复制。
- **Convertible<X,Y>**: 一个 **X** 可以隐式转换为一个 **Y**。
- **Common<X,Y>**: 一个 **X** 和一个 **Y** 可以无歧义地转换为一个称为 **Common_type<X,Y>** 的公共类型。这是语言规则对 ?: 运算数兼容性的形式化（§11.1.3）。例如，**Common_type<Base_*,Derived_*>** 是 **Base_*** 并且 **Common_type<int,long>** 是 **long**。
- **Range<X>**: 一个 **X** 可以被 rangefor 使用（§9.5.1），也就是说，**X** 必须提供成员 **x.begin()** 和 **x.end()**，或非成员等价物 **begin(x)** 和 **end(x)**，具有所需语义。

显然，这些定义是不正式的。在大多数情况下，这些概念基于标准库类型谓词（§35.4.1），并且 ISO C++ 标准提供了正式定义（例如，§iso.17.6.3）。

## 24.4.5 Template Definition Checking

约束检查模板确保类型提供了概念所需属性。如果模板的实现实际上使用了超出其概念保证的属性，我们可能会得到类型错误。例如，标准库 find() 要求一对输入迭代器作为参数，但我们可能会（不谨慎地）像这样定义它：

```
template<typename Iter, typename Val>
Iter find(Iter b, Iter e, Val x)
{
static_assert(Input_iterator<Iter>(),"find(): Iter is not a Forward iterator");
static_assert(Equality_comparable<Value_type<Iter>,Val>, "find(): value type doesn’t match iterator");

while (b!=e) {
if (*b==x) return b;
b = b+1; // note: not ++b
}
return b;
}
```

现在，b+1 是一个错误，除非 b 是一个随机访问迭代器（而不仅仅是约束检查所保证的前向迭代器）。然而，约束检查并不能帮助我们检测该问题。例如：

```
void f(list<int>& lst, vector<string>& vs)
{
auto p = find(lst.begin(),lst.end(),1209); // error :list does not provide + auto q =
find(vs.begin(),vs.end(),"Cambridge"); // OK: vector provides +
//...
}
```

对 list 的 find() 调用将失败（因为 + 未为 list 提供的前向迭代器定义），而对 vector 的调用将成功（因为 b+1 对 vector<string>::iterator 是可以的）。

约束检查主要为模板的用户提供服务：实际的模板参数会根据模板的要求进行检查。另一方面，约束检查并不能帮助希望确保实现不使用超出概念中指定的属性的模板编写者。理想情况下，类型系统会确保这一点，但这需要仍在未来语言特性中。所以，我们如何测试参数化类或通用算法的实现？

概念提供了一个强有力的指导：实现不应使用参数的任何属性，而这些属性未由概念指定，因此我们应该使用仅提供实现概念所指定的属性的论证来测试实现，而仅限于这些属性。这种类型有时被称为原型。

因此，对于 find() 示例，我们查看 Forward_iterator 和 Equality_comparable 或标准的关于前向迭代器和相等可比较概念的定义（§iso.17.6.3.1, §iso.24.2.5）。然后，我们决定需要一个 Iterator 类型至少提供：

- 一个默认构造函数
- 一个拷贝构造函数和拷贝赋值
- 运算符 == 和 !=
- 前缀运算符 ++
- 一个类型 Value_type<Iterator>
- 前缀运算符 *
- 将 * 的结果赋给 Value_type<Iterator> 的能力
- 将 Value_type<Iterator> 赋给 * 的结果的能力

这与标准库前向迭代器相比略有简化，但足以用于 find()。通过查看概念来构建该列表很容易。

给定这个列表，我们需要找到或定义一个类型，它仅提供所需的功能。对于 find() 所需的前向迭代器，标准库 forward_list 完全符合要求。这是因为“前向迭代器”被定义为表达可以遍历单链表的东西的概念。并不少见，流行类型是流行概念的原型。如果我们决定使用现有类型，我们必须小心，不要选择比所需更灵活的类型。例如，测试算法（如 find()）时典型的错误是使用 vector。然而，

