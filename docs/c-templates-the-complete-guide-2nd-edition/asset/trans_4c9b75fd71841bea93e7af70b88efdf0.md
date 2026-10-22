
注意，函数模板`get`仅仅是对`TupleGet`的静态成员函数调用的一个薄封装。该技术实际上是对函数模板缺乏部分特化的一种变通方法（在第356页的17.3节中讨论），我们用它来针对N的值进行特化。在递归情形（N > 0）中，静态成员函数`apply()`提取当前元组的尾部，并将N递减以继续在元组中更靠后的位置查找所需元素。基础情形（N = 0）返回当前元组的头部，从而完成实现。

## 25.1.2 构造

除了目前已经定义的构造函数：[点击此处查看代码图像](#)

```
Tuple() {
}
Tuple(Head const& head, Tuple<Tail...> const& tail)
  : head(head), tail(tail) {
}
```

为了使元组实用，我们需要能够从一组独立值（每个元素对应一个值）以及从另一个元组来构造它。从一组独立值进行拷贝构造时，会将这些值中的第一个传递给头部元素（通过其基类）以进行初始化，然后将剩余值传递给代表尾部的基类：[点击此处查看代码图像](#)

```
Tuple(Head const& head, Tail const&... tail)
  : head(head), tail(tail...) {
}
```

这使得我们最初的Tuple示例得以工作：[点击此处查看代码图像](#)

```
Tuple<int, double, std::string> t(17, 3.14, "Hello World!");
```

然而，这并非最通用的接口：用户可能希望使用移动构造来初始化部分（但可能不是全部）元素，或者希望某个元素由不同类型的值构造而来。因此，我们应该使用完美转发（第280页的15.6.3节）来初始化元组：[点击此处查看代码图像](#)

```
template<typename VHead, typename... VTail>
Tuple(VHead&& vhead, VTail&&... vtail)
  : head(std::forward<VHead>(vhead)),
    tail(std::forward<VTail>(vtail)...) {
}
```

接下来，我们实现从另一个元组构造元组的支持：点击此处查看代码图像

```
template<typename VHead, typename... VTail>
Tuple<Tuple<VHead, VTail...> const& other)
: head(other.getHead()), tail(other.getTail()) { }
```

然而，引入该构造函数并不足以支持元组转换：对于上面的元组t，尝试创建另一个具有兼容类型的元组将失败：点击此处查看代码图像

```
// ERROR: no conversion from Tuple<int, double, string> to long
Tuple<long int, long double, std::string> t2(t);
```

问题在于，用于从一组独立值初始化的构造函数模板比接受元组的构造函数模板匹配得更好。为了解决这个问题，我们必须使用`std::enable_if<>`（参见第98页的6.3节和第469页的20.3节），在尾部长度不符合预期时禁用这两个成员函数模板：点击此处查看代码图像

```
template<typename VHead, typename... VTail,
typename = std::enable_if_t<sizeof...(VTail)==sizeof...(Tail)>>

Tuple(VHead&& vhead, VTail&&... vtail)
: head(std::forward<VHead>(vhead)),
tail(std::forward<VTail>(vtail)...) { }
```

```
template<typename VHead, typename... VTail,
typename = std::enable_if_t<sizeof...(VTail)==sizeof...(Tail)>>
Tuple<Tuple<VHead, VTail...> const& other)
: head(other.getHead()), tail(other.getTail()) { }
```

你可以在`tuples/tuple.hpp`中找到所有构造函数的声明。

`makeTuple()`函数模板利用推导来确定其返回的Tuple的元素类型，使得从给定的一组元素创建元组变得容易得多：点击此处查看代码图像

tuples/maketuple.hpp

```
template<typename... Types>
auto makeTuple(Types&&... elems)
{
return Tuple<std::decay_t<Types>...>(std::forward<Types>(elems)...);
}
```

同样，我们将完美转发与`std::decay<>`特征结合使用，以

将字符串字面量和其他原始数组转换为指针，并移除const和引用。例如：点击此处查看代码图像

```
makeTuple(17, 3.14, "Hello, World!") initializes a
```

点击此处查看代码图像

```
Tuple<int, double, char const*>
```

## 25.2 基本元组操作

### 25.2.1 比较

元组是包含其他值的结构类型。要比较两个元组，只需比较它们的元素即可。因此，我们可以编写一个`operator==`的定义，逐元素地比较两个元组：点击此处查看代码图像

tuples/tupleeq.hpp

```
// basis case:
bool operator==(Tuple<> const&, Tuple<> const&)
{
// empty tuples are always equivalent
return true;
}
// recursive case:
template<typename Head1, typename... Tail1,
typename Head2, typename... Tail2,
typename = std::enable_if_t<sizeof...(Tail1)==sizeof...(Tail2)>>
bool operator==(Tuple<Head1, Tail1...> const& lhs,
Tuple<Head2, Tail2...> const& rhs)
{
return lhs.getHead() == rhs.getHead() &&
lhs.getTail() == rhs.getTail();
}
```

与许多作用于类型列表和元组的算法一样，逐元素比较会先访问头部元素，然后递归访问尾部，最终到达基础情形。`!=`、`<`、`>`、`<=`和`>=`运算符也类似地实现。

### 25.2.2 输出

重排元组中的元素，或选择元组中的某些元素子集。

元组算法特别有趣，因为它们同时需要编译期和运行期的计算。与第24章的类型列表算法一样，对元组应用算法可能会产生一个类型完全不同的元组，这需要编译期计算。例如，反转`Tuple<int, double, string>`会生成`Tuple<string, double, int>`。然而，与针对同质容器的算法（例如对`std::vector`应用`std::reverse()`）一样，元组算法实际上需要代码在运行期执行，因此我们需要注意生成代码的效率。

### 25.3.1 元组作为类型列表

如果我们忽略`Tuple`模板中实际的运行期组成部分，就会发现它与第24章中开发的`Typelist`模板具有完全相同的结构：它接受任意数量的模板类型参数。实际上，通过少量的部分特化，我们就可以将`Tuple`变成一个功能完备的类型列表：点击此处查看代码图像

tuples/tupletypelist.hpp

```
// determine whether the tuple is empty:
template<>
struct IsEmpty<Tuple<>> {
static constexpr bool value = true;
};

// extract front element:
template<typename Head, typename... Tail>
class FrontT<Tuple<Head, Tail...>> {
public:
using Type = Head;
};
// remove front element:
template<typename Head, typename... Tail>
class PopFrontT<Tuple<Head, Tail...>> {
public:
using Type = Tuple<Tail...>; 
};

// add element to the front:
template<typename... Types, typename Element>
```

```
class PushFrontT<Tuple<Types...>, Element> {
public:
using Type = Tuple<Element, Types...>;
};
```

// 在尾部添加元素：

```
template<typename... Types, typename Element>
class PushBackT<Tuple<Types...>, Element> {
public:
using Type = Tuple<Types..., Element>;
};
```

现在，第24章中开发的所有类型列表算法都可以同样好地作用于`Tuple`和`Typelist`，因此我们可以轻松地处理元组的类型。例如：点击此处查看代码图像

```
Tuple<int, double, std::string> t1(17, 3.14, "Hello, World!");
using T2 = PopFront<PushBack<decltype(t1), bool>>;
T2 t2(get<1>(t1), get<2>(t1), true);
std::cout << t2;
```

它将打印：

```
(3.14, Hello, World!, 1)
```

稍后我们将看到，应用于元组类型的类型列表算法常常用来帮助确定元组算法的结果类型。

### 25.3.2 向元组添加元素和从元组移除元素

对于元组的值而言，能够在元组的开头或末尾添加元素对于构建更高级的算法非常重要。与类型列表一样，在元组前部插入远比在后部插入容易，因此我们从`pushFront`开始：点击此处查看代码图像

tuples/pushfront.hpp

```
template<typename... Types, typename V>
PushFront<Tuple<Types...>, V>
pushFront(Tuple<Types...> const& tuple, V const& value)
{
return PushFront<Tuple<Types...>, V>(value, tuple);
}
```

将一个新元素（称为value）添加到现有元组的前部
