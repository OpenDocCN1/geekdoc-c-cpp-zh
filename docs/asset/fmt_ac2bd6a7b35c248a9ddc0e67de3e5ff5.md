
# priority_queue

优先级队列是一种保持元素有序的队列。它不是遵循严格的 FIFO（先入先出）顺序，而是在队列头部的元素始终是优先级最高的那个。这个元素可能是队列中最老的，也可能是最近的。如果两个元素的优先级相等，它们在队列中的相对顺序是定义的。

`priority_queue` 容器适配器也定义在 `<queue>` 中。它的模板定义看起来如下（仅为偏移）：

```cpp
template <class T, class Container = Vector<T>, class Compare = less<T> >;
```

它并没有看起来那么复杂。你已经见过前两个参数：`T` 是存储在 `priority_queue` 中的元素类型，`Container` 是 `priority_queue` 适配的底层容器。`priority_queue` 使用 `vector` 作为默认，但 `deque` 运行良好。`list` 无法工作，因为 `priority_queue` 要求对其元素进行随机访问。第三个参数 `Compare` 比较复杂。你将在第 17 章学习更多关于它的信息，`less` 是一个类模板，支持使用 `operator<` 比较两个类型为 `T` 的对象。对你来说，这意味着队列中元素的优先级是根据 `operator<` 决定的。你可以自定义所使用的比较方法，但那是 17 章的话题。请为 `priority_queue` 中存储的类型适当定义 `operator<`。

`priority_queue` 的头部元素默认情况下是优先级最高的元素，根据 `operator<` 使得“小于”其他元素的元素优先级较低。

## priority_queue 操作

`priority_queue` 提供的操作比队列少。`push()` 和 `emplace` 方法允许你插入元素，`pop()` 允许你移除元素，而 `top()` 返回头部元素的 const 引用。

> 注意：`pop()` 不返回被弹出的元素。如果你想保留副本，必须先通过 `top()` 获取它。

`priority_queue` 支持 `size()`、`empty()` 和 `swap()`。然而，它不提供任何比较运算符。

## priority_queue 示例：错误处理器

系统中的故障经常会从不同组件产生错误。良好的错误处理系统使用 `priority_queue` 来优先处理最重要的错误。你可以写一个简单的处理器。假设所有错误都编码了优先级。以下是类定义：

```cpp
// 带有优先级和字符串描述的 Error 类。
class Error {
public:
    Error(int priority, const std::string& errMsg)
        : priority(priority), mErr(errMsg) {}
    int getPriority() const { return priority; }
    const std::string& getError() const { return mErr; }
    friend operator<(const Error& lhs, const Error& rhs);
    friend std::ostream& operator<<(std::ostream& os, const Error& err);
private:
    int priority;
    std::string mErr;
};
// 优先返回错误的处理器 类。
class ErrorCorrelator {
public:
    // 添加错误。
    void addError(const Error& error);
    // 获取下一个要处理的错误。
    Error getError();
private:
    std::priority_queue<Error> mErrors;
};
```

以下是函数和方法的定义：

```cpp
bool operator<(const Error& lhs, const Error& rhs) {
    return (lhs.getPriority() < rhs.getPriority());
}
ostream& operator<<(std::ostream& os, const Error& err) {
    os << err.getError() << " (priority " << err.getPriority() << ")";
    return os;
}
void ErrorCorrelator::addError(const Error& error) {
    mErrors.push(error);
}
Error ErrorCorrelator::getError() {
    // 如果没有更多错误，抛出异常。
    if (mErrors.empty()) {
        throw std::out_of_range("没有更多错误.");
    }
    // 保存头部元素。
    Error top = mErrors.top();
    // 移除头部元素。
    mErrors.pop();
    // 返回保存的元素。
    return top;
}
```

这是一个显示如何使用 `ErrorCorrelator` 的单元测试。实际应用需要多个线程，一个线程添加错误，其他线程处理它们。正如之前队列示例中提到的，这需要第 23 章讨论的显式同步。

```cpp
ErrorCorrelator ec;
ec.addError(3, "无法读取文件");
ec.addError(1, "用户输入错误");
ec.addError(10, "无法分配内存！");
while (true) {
    try {
        Error e = ec.getError();
        cout << e << endl;
    } catch (const out_of_range& e) {
        cout << "处理完成错误" << endl;
        break;
    }
}
```

该程序的输出如下：

```
无法分配内存！ (priority 10)
无法读取文件 (priority 3)
用户输入错误 (priority 1)
处理完成错误
```

# stack

栈与队列几乎相同，但它提供了*先入后出*（FILO）语义，也称为*后入先出*（LIFO），而不是 FIFO。它定义在 `<stack>` 头文件中。模板定义如下：

```cpp
template <class T, class Container = deque<T>> class stack;
```

你可以使用 *vector,list,* 或 `deque` 作为栈的底层容器。

## stack 操作

与队列一样，栈提供了 `push()`、`emplace()` 和 `pop()`。区别在于 `push()` 将新元素添加到栈的顶部，“压入”所有较早插入的元素，而 `pop()` 从栈的顶部移除元素，即最近插入的元素。`top()` 方法在*const* 对象上调用时返回头部元素的 *const* 引用，在非*const* 对象上调用时返回非*const*引用。

> 注意：`pop()` 不返回被弹出的元素。如果你想保留副本，必须先通过 `top()` 获取它。

栈支持 `empty()`、`size()`、`swap()` 和标准比较运算符。

## stack 示例：修订后的错误处理器

你可以重写 `ErrorCorrelator` 类，使其输出最近的错误而不是优先级最高的错误。唯一的更改是将 `mErrors` 从 `priority_queue` 改为 `stack`。通过此更改，错误将按照 LIFO 顺序而不是优先级顺序分布。方法定义不需要更改，因为 `push()`、`pop()`、`top()` 和 `empty()` 在 `priority_queue` 和栈中都存在。

# 关联容器

与顺序容器不同，关联容器不以线性配置存储元素。相反，它们提供了键到值的映射。它们通常提供相等的插入、删除和查找时间。

STL 提供了四个关联容器：`map`、`multimap` 和 `multiset`。这些容器中的每个元素都存储在*排序的*、树形的数据结构中。还有四个无序关联容器：`unordered_map`、`unordered_multimap`、`unordered_set` 和 `unordered_multiset`。这些将在本章稍些时候讨论。

## pair 工具类

在学习关联容器之前，你必须熟悉 `<utility>` 头文件。`pair` 是一个将两个类型值组合在一起的类模板。这些值可以通过公共 `first` 和 `second` 访问。

成员变量。`pair` 定义了 `operator==` 和 `operator<`，用于比较第一个元素和第二个元素。以下是一些示例：

```
// 两个参数构造函数和默认构造函数
pair<string, int> myPair("hello", 5);
pair<string, int> myOtherPair;
// 可以直接赋值 first 和 second
myOtherPair.first = "hello";
myOtherPair.second = 6;
// 拷贝构造函数
pair<string, int> myThirdPair(myOtherPair);
if (myPair < myOtherPair) {
    cout << "myPair is less than myOtherPair" << endl;
} else {
    cout << "myPair is greater than or equal to myOtherPair" << endl;
}
if (myPair == myThirdPair) {
    cout << "myOtherPair is equal to myThirdPair" << endl;
} else {
    cout << "myPair is not equal to myThirdPair" << endl;
}
```

输出如下：

```
myPair is less than myOtherPair
myPair is equal to myOtherPair
```

该库提供了一个实用函数模板 `make_pair()`，它可以从两个值构造一个 `pair`。例如：

```
pair<int, int> a = make_pair(5, 10);
```

在这种情况下，你本可以使用两个参数的构造函数。然而，当你想要将 `pair` 传递给函数或将其赋值给已存在的变量时，`make_pair()` 更有用。与类模板不同，函数模板可以从参数推推类型，因此你可以使用 `make_pair()` 在不显式指定类型的情况下构造 `pair`。你可以如下使用 `auto` 关键字：

```
auto aSecondPair = make_pair(5, 10);
```

> 警告 在 `pair` 中使用原始指针类型（plain old pointer types）是有风险的，因为 `pair` 的拷贝构造函数和赋值运算符仅对指针类型执行浅拷贝和赋值。但是，你可以安全地在 `pair` 中存储像 `shared_ptr` 这样的智能指针。

# map

定义在 `<map>` 头文件 `map` 存储的是键值对（key/value pairs）而不是单个值。插入、查找和删除都基于键（key）；值（value）是附带的。“map”一词源于概念性理解，即该容器将键“映射”（maps）到值。

`map` 根据键对元素保持排序顺序，因此插入、删除和查找的时间复杂度均为对数级。因为当我们枚举元素时，它们是按照类型 `operator<` 或用户定义的比较器所施加顺序输出的。它通常被实现为某种形式的平衡树，例如红黑树。然而，树结构对客户端是的。

每当你需要根据“键”存储和检索元素，并希望它们按特定顺序排列时，就应该使用 `map`。

## 构建 map

`map` 模板接受四种类型：键类型、值类型、比较类型和分配器类型。一如既往，本章中忽略了分配器。比较类型与之前描述的 `priority_queue` 的比较类型相似。它允许你指定一个与默认不同的比较类。在本章中，使用了默认的 `less` 比较。使用默认值时，确保你的键恰当地响应 `operator<`。如果你对更多细节感兴趣，第 17 章解释了如何编写自己的比较器类。

如果你忽略比较和分配器参数，构建 `map` 就像构建 `vector` 或 `list` 一样，不同在于你在模板中分别指定了键和值类型。例如，以下代码构建了一个使用 `int` 作为键并存储 `Data` 类对象的 `map`：

```
class Data {
public:
    explicit Data(int val = 0) { mVal = val; }
    int getVal() const { return mVal; }
    void setVal(int val) { mVal = val; }
private:
    int mVal;
};
map<int, Data> data;
```

`map` 也支持统一初始化：

```
map<string, int> m = {
    "Marc.", 123,
    "Warren B.", 456,
    "Peter V.", 789
};
```

## 插入元素

向 `vector` 或 `list` 等顺序容器插入元素总是需要指定元素所在的位置。`map` 与其他关联容器不同，它的 `insert()` 方法接受一个迭代器作为提示（hint），这决定了容器存储元素的位置。

## 关联容器

插入元素时，请记住 `map` 要求键是唯一的：如果你想支持具有相同键的元素，你有两种选择。你可以使用 `vector` 或数组作为键的容器，或者使用稍后描述的 `multimap`。

向 `map` 插入元素有两种方法：一种笨拙，一种不那么笨拙。

## insert() 方法

向 `map` 添加元素的笨担方法是 `insert()` 方法，但它的优点是允许你检测键是否已存在。一个问题是返回值，它包含一个迭代器和一个指示是否插入成功的布尔值。

更优雅的插入方法是使用下标运算符 `[]`。然而，这种方法不会告诉你元素是否已存在；它只会覆盖现有值。如果你需要知道插入是否成功，请使用 `insert()` 方法。

```cpp
map<string, int> counts;
auto result = counts.insert({"apple", 1});
if (result.second) {
    cout << "Inserted apple" << endl;
} else {
    cout << "Apple already exists" << endl;
}
```

或者，你可以使用带有提示的 `insert()` 方法，如果你知道元素在 `map` 中的预期位置，这样效率更高。

```cpp
counts.insert(counts.end(), {"banana", 2});
```

## operator[]

下标运算符 `[]` 为 `map` 插入或更新元素提供了方便的方法。如果键存在，该运算符返回关联值的引用。如果键不存在，它将插入一个具有该键和默认值的新元素。

然而，`operator []` 不能用于 `const` `map`，因为它可能会修改 map。对于 `const` `map`，请使用 `find()` 或 `at()` 方法。

```cpp
map<string, int> inventory;
inventory["apples"] = 10; // 如果键不存在则插入
inventory["apples"] = 20; // 如果键存在则更新
```
```cpp
void printInventory(const map<string, int>& inv) {
    for (const auto& [key, value] : inv) {
        cout << key << ": " << value << endl;
    }
}
```

> 警告 你可以通过非 const 迭代器修改元素的值，如果你尝试修改元素的键（即使通过非 const 迭代器），编译器将生成一个错误，因为这会破坏 map 中元素的排序顺序。

`map` 迭代器是双向的，这意味着你可以向两个方向上遍历它们。

## 查找元素

`map` 根据所提供的键对元素进行对数级查找。如果你已经知道具有给定键的元素在 `map` 中，那么最简单的查找方法是通过运算符 `operator []`，只要你是在非 const `map` 或对 `map` 的非 const 引用上调用它即可。`operator []` 的用处是它返回一个元素的引用，你可以直接使用并修改它，而无需担心从 `pair` 对象中提取值。这里是前一个示例的扩展，用于对键为 1 的 `Data` 对象值调用 `setValue()` 方法：

```cpp
map<int, Data> dataMap;
dataMap[1] = Data(4);
dataMap[1] = Data(6);
dataMap[1].setValue(100);
```

如果你不知道某个元素是否存在，你可能不想使用 `operator []`，因为如果找不到，它将插入一个带有你的键的新元素。作为替代方案，`map` 提供了 `find()` 方法，它返回一个指向指定键元素的迭代器（如果存在），如果不在 `map` 中，则返回 `end()` 迭代器。这里是一个使用 `find()` 对键为 1 的 `Data` 对象进行相同修改的示例：

```cpp
auto it = dataMap.find(1);
if (it != end(dataMap)) {
  it->second.setValue(100);
}
```

如你所见，`find()` 有点笨拙，但有时是必要的。
