
作为一个具体示例，假设错误是因为对一个空栈执行弹出操作而触发的。为了引发这一事件，`Stack` 调用了以下代码（实际实现略有不同，因为 `Stack` 被封装在 pimpl 中）：

```
parent_..raise(Stack::StackError,
make_shared<StackEventData>(
StackEventData::ErrorConditions::Empty));
```

`raise()` 函数的第一个参数是一个解析为 `"error"` 的静态字符串。回顾一下，为了处理多个事件，发布者会为每个事件命名。在这里，`Stack::StackError` 静态变量保存的就是该事件的名称。使用变量而非直接使用字符串，是为了防止因事件名称输入错误而导致运行时错误。`raise()` 函数的第二个参数创建 `StackEventData` 实例，并用空栈错误条件对其初始化。请注意，该实现使用 `shared_ptr` 传递事件数据。这一决定将在下面关于共享语义的边栏中讨论。虽然 `StackObserver` 类尚未引入，但为了完整性，我指出事件可以通过以下典型代码进行处理：

```
StackObserver::notify(shared_ptr<EventData> d)
{
shared_ptr<StackEventData> p =
dynamic_pointer_cast<StackEventData>(d);
if(p) {

// do something with the data }
else
{

// uh oh, what event did we just catch?! }
}
```

## 现代 C++ 设计说明：共享语义与 shared_ptr

`unique_ptr` 使程序员能够安全地表达唯一所有权，而 `shared_ptr` 使程序员能够安全地表达共享所有权。在 C++11 标准之前，C++ 通过原始指针或引用实现数据共享。由于类数据的引用只能在构造期间初始化，因此对于后期绑定的数据，只能使用原始指针。所以，两个类常常各自包含一个指向公共对象的原始指针，从而共享同一份数据。这种场景的问题显然在于：不清楚哪个对象拥有这个共享对象。尤其地，这种模糊性意味着不确定何时可以安全地删除这样的共享对象，以及最终应该由哪个拥有者释放内存。`shared_ptr` 在标准库层面解决了这个难题。`shared_ptr` 通过引用计数实现共享语义。当新对象指向一个 `shared_ptr` 时，内部引用计数会增加（通过构造函数和赋值操作强制执行）。当 `shared_ptr` 离开作用域时，其析构函数被调用，从而使内部引用计数递减。当计数降至零时，最后一个 `shared_ptr` 的析构会触发底层内存的回收。与 `unique_ptr` 一样，显式成员函数调用也可以（提前释放内存）。事件处理完成后，发布者不能简单地在事件已被处理后释放内存。此外，由于任何给定事件都可能调用多个观察者，发布者也不能将数据的唯一所有权转移给任何特定观察者。因此，C++11 中标准化的 `shared_ptr` 为处理这种情况提供了理想的语义。

现在你已经理解了事件数据，让我们最终编写抽象 `Observer` 接口。不出所料，它正是你可能期待的样子。参见清单 3-5。

## 清单 3-5. 抽象 Observer 接口

```
class Observer
{
public :

explicit Observer(const string& name);
virtual ~Observer();
virtual void notify(shared_ptr<EventData>) = 0;
```

## 作为事件发布者的 Stack

构造 `Stack` 的最后一步，就是将各部分组合到一起。清单 3-1 展示了作为单例的 `Stack`。为了实现事件，我们只需修改这段代码，使其继承 `Publisher` 基类。现在我们必须问自己：这种继承应该是公有继承还是私有继承？

通常，在面向对象编程中，人们使用公有继承来表达 is-a 关系。也就是说，公有继承表达的是派生类是基类的一种类型或特化。更准确地说，is-a 关系遵循里氏替换原则（LSP）[29]，该原则指出（通过多态），接受基类指针（或引用）作为参数的函数，必须能够在不知道的情况下接受派生类指针（或引用）。简而言之，在可以使用基类的任何地方，派生类都必须可以互换使用。当人们提到继承时，通常指的是公有继承。

私有继承用于表达 implements-a 关系。简单地说，私有继承用于将一个类的实现嵌入到另一个类的私有实现中。它不遵循 LSP，而且事实上，如果继承关系是私有的，C++ 语言不允许将派生类替换为基类。为了完整起见，与之密切相关的受保护继承在语义上与私有继承相同。唯一区别在于，私有继承中基类的实现在派生类中变为私有，而受保护继承中基类的实现在派生类中变为受保护。

我们的问题现在可以细化为：`Stack` 是一个 `Publisher`，还是 `Stack` 实现了 `Publisher`？答案是“是”和“是”。这没什么帮助，那么我们该如何选择？

为了在这种情形下消除公有继承或私有继承的歧义，我们必须更深入考察 `Stack` 类的使用方式。公有继承（即 is-a 关系）表明我们意图将栈作为发布者以多态方式使用。但事实并非如此。虽然 `Stack` 类是发布者，但它在 LSP 意义上并不是一个可以替换为 `Publisher` 的发布者。因此，我们应该使用私有继承，以表明在 `Stack` 内部使用 `Publisher` 实现的意图。等价地，我们可以说 `Stack` 提供了 `Publisher` 服务。如果你一直在跟随仓库中的源代码，你可能已经注意到一个大提示：私有继承才是答案。`Publisher` 类是用非虚的受保护析构函数实现的，这使得它无法用于公有继承。

熟悉面向对象设计的读者可能会问，为什么我没有问那个无处不在的 has-a 问题，它表示所有权或聚合关系。也就是说，为什么 `Stack` 不直接拥有一个 `Publisher` 并复用其实现，而是私有继承它？许多设计者几乎完全倾向于用聚合代替私有继承，他们认为，当在这两者之间进行等价选择时，人们应该始终选择带来更松耦合的语言特性（继承是比聚合更强的关联）。这种观点有其道理。不过就我个人而言，我只是倾向于接受以更强耦合换取更高清晰度的技巧。我相信私有继承比聚合更清楚地表达了实现 `Publisher` 服务的设计意图。这个决定没有对错之分。在你的代码中，你应该选择适合你个人品味的风格。

私有继承自 `Publisher` 类的另一个后果是，`Publisher` 的 `attach()` 和 `detach()` 方法变成了私有方法。然而，如果任何其他类打算订阅 `Stack` 的事件，它们就必须是 `Stack` 公共接口的一部分。因此，实现者必须选择使用 using 声明或转发成员函数，将 `attach()` 和 `detach()` 提升到 `Stack` 的公共接口。这两种方法在此上下文中都是可接受的，实现者可以自由选择他或她偏好的方式。

## 完整的 Stack 接口

我们终于准备好编写完整的 `Stack` 公共接口了。参见清单 3-6。

**清单 3-6.** 完整的 Stack 公共接口

```
class Stack : private Publisher
{
public:

static Stack& Instance();

void push(double, bool suppressChangeEvent = false); double pop(bool suppressChangeEvent = false);
void swapTop();
vector<double> getElements(size_t n) const;

using Publisher::attach;
using Publisher::detach;
```
