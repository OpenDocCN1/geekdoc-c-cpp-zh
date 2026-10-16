

invoked.

这意味着在遵循这种简单的资源获取模型时，构造器的作者无需编写显式的异常处理代码。
最常见的资源是内存，而 string、vector 以及其他标准容器都使用 RAII 来隐式管理获取和释放。与使用 new（并且可能还有 delete）进行特设内存管理相比，这节省了大量工作并避免了大量错误。
当需要指向对象的指针而不是局部对象时，请考虑使用标准库类型 unique_ptr 和 shared_ptr（§5.2.1，§34.3）来避免泄漏。

## 13.3.1 Finally

将资源表示为带析构函数的类对象所需的纪律让一些人感到困扰。一次又一次，人们为在异常发生后编写任意清理代码而发明了“finally”语言结构。这种技术通常不如 RAII，因为它们是特设的，但如果你真的想要特设，RAII 也能提供。 首先，我们定义一个类，它将在析构函数中执行任意操作。

```
template<typename F>
struct Final_action {
Final_action(F f): clean{f} {}
~Final_action() { clean(); }
F clean;
};
```

“finally action”作为参数传递给构造函数。

接下来，我们定义一个方便推导操作类型 的函数：

```
template<class F>
Final_action<F> finally(F f)
{
return Final_action<F>(f);
}
```

最后，我们可以测试 finally()：

```
void test()
// handle undisciplined resource acquisition // demonstrate that arbitrary actions are possible
{
int* p = new int{7};
int* buf=(int*)malloc(100*sizeof(int));
// probably should use a unique_ptr (§5.2) // C-style allocation
auto act1 = finally([&]{ delete p; free(buf); // C-style deallocation cout<< “Goodby, Cruel world!\n”;
```

（以及类似的条件）：

- *就别那么做：* 满足前置条件是调用者的职责，如果调用者没有做到，就让不良结果发生——最终这些错误会通过改进设计、调试和测试从系统中消除。
- *终止程序：* 违反前置条件是一个严重的设计错误，在存在此类错误的情况下程序不得继续。希望整个系统能够从一个组件（该程序）的失败中恢复——最终这类故障可能也会通过改进设计、调试和测试从系统中消除。

为什么有人会选择这些替代方案之一？第一种方法通常与性能需求有关：系统地检查前置条件可能导致对逻辑上不必要的条件的重复测试（例如，如果调用者已正确验证数据，则成千上万个被调用函数中的数百万次测试在逻辑上可能是冗余的）。性能上的成本可能很显著。为了获得这种性能，在测试期间承受反复崩溃可能是值得的。显然，这假设你最终能将所有关键的前置条件违规从系统中清除。对于一些系统，通常是完全由一个组织控制的系统，这是一个现实的目标。

第二种方法倾向于用于在前置条件失败时认为完全且及时的恢复不可行的系统。也就是说，确保恢复是完整的，会给系统设计和实现带来不可接受的复杂性。另一方面，终止程序被认为是可以接受的。例如，如果重新运行程序并使用使重复失败不太可能发生的输入和参数很容易，那么将程序终止视为可接受是合理的。一些分布式系统就是这样（只要终止的程序只是完整系统的一部分），我们为自己消费编写的许多小型程序也是如此。

现实中，许多系统使用异常和这两种替代方法 的混合。 三者都共享这样一个共同观点：前置条件应被定义并遵守；不同之处在于执行方式以及是否认为恢复是可行的。程序结构可能因是否以（局部）恢复为目标而截然不同。在大多数系统中，一些异常是在根本不期望恢复的情况下抛出的。例如，我经常抛出异常以确保某些错误日志记录或在终止或重新初始化进程之前生成一个体面的错误消息（例如，从 main() 中的 catch(...)）。

表达对期望条件和不变量的检查使用了各种技术。当我们想对检查的逻辑原因保持中立时，我们通常使用断言一词，通常缩写为 assert。断言只是一个被假定为真的逻辑表达式。然而，为了使断言不仅仅是一条注释，我们需要一种表达如果它为假时会发生什么的方法。查看各种系统，我看到在表达断言时有各种需求：

- 我们需要在编译时断言（由编译器评估）和运行时断言（在运行时评估）之间进行选择。
- 对于运行时断言，我们需要在 throw、terminate 或 ignore 之间进行选择。
- 除非某个逻辑条件为真，否则不应生成任何代码。例如，某些运行时断言只有在逻辑条件为真时才应被评估。通常，逻辑条件是类似调试标志、检查级别或用于在要强制执行的断言之间选择的掩码之类的东西。
- 断言不应冗长或复杂编写（因为它们可能非常常见）。并非每个系统都需要或支持每种替代方案。

标准提供了两种简单机制：

- 在 <cassert> 中，标准库提供了 assert(A) 宏，如果宏 NDEBUG（“not debugging”）未定义，则在运行时检查其断言 A（§12.6.2）。如果断言失败，编译器会输出包含（失败的）断言、源文件名和源文件行号的错误消息并终止程序。
- 语言提供了 static_assert(A,message)，它无条件地在编译时检查其断言 A（§2.4.3.3）。如果断言失败，编译器会输出消息并且编译失败。

当 assert() 和 static_assert() 不足时，我们可以使用普通代码进行检查。例如：

```
void f(int n)
// n should be in [1:max)
{
if (2<debug_level && (n<=0 || max<n) throw Assert_error("range problem"); // ...
```

然而，使用这种“普通代码”往往会模糊正在测试的内容。我们是：

- 评估我们测试的条件吗？（是的，2<debug_level 部分。）
- 评估一个条件，该条件对于某些调用预期为真，对于其他调用不为真吗？（否，因为我们抛出异常——除非有人试图将异常仅用作另一种返回机制；§13.1.4.2。）
- 检查一个永远不应失败的前置条件吗？（是的，异常只是我们选择的响应。）

更糟糕的是，前置条件测试（或不变量测试）很容易分散到其他代码中，从而更难发现也更容易出错。我们希望有一个可识别的机制来检查断言。以下是一个（可能有点过于复杂）用于表达各种断言和对失败的各种响应的机制。首先，我定义了决定何时测试以及断言失败时该做什么的机制：

```
namespace Assert {
enum class Mode { throw_, terminate_, ignore_ };
constexpr Mode current_mode = CURRENT_MODE;
constexpr int current_level = CURRENT_LEVEL;
constexpr int default_level = 1;

constexpr bool level(int n) { return n<=current_level; }
struct Error : runtime_error {
Error(const string& p) :runtime_error(p) {} };
// ...
}
```

想法是只要断言的“级别”低于或等于 `current_level` 就进行测试。如果断言失败，则使用 `current_mode` 在三种替代方案中进行选择。`current_level` 和 `current_mode` 是常量，因为想法是除非我们做出决定，否则根本不为断言生成任何代码。想象 `CURRENT_MODE` 和 `CURRENT_LEVEL` 在程序的构建环境中设置，可能作为编译器选项。

程序员将使用 `Assert::dynamic()` 来进行断言：

```
namespace Assert {
// ...

string compose(const char * file, int line, const string& message) // compose message
including file name and line number
{
ostringstream os ("(");
os << file << "," << line << "):" << message; return os.str();
template<bool condition =level(default_level), class Except = Error> void
dynamic(bool assertion, const string& message ="Assert::dynamic failed")
{
if (assertion)
return;
if (current_mode == Assert_mode::throw_) throw Except{message};
if (current_mode == Assert_mode::terminate_) std::terminate();
}

template<>
void dynamic<false ,Error>(bool, const string&) // do nothing {
}

void dynamic(bool b, const string& s) // default action
{
dynamic<true ,Error>(b,s);
}

void dynamic(bool b) // default message
{
dynamic<true ,Error>(b);
}
}
```

我选择了名称 `Assert::dynamic`（意为“在运行时评估”）以与 `static_assert`（意为“在编译时评估”；§2.4.3.3）形成对比。

可以进一步使用实现技巧来最小化生成的代码量。或者，如果需要更多灵活性，我们可以在运行时进行更多测试。这个 `Assert` 不是标准的一部分，主要作为说明问题和实现技术的示例。我怀疑断言机制的需求变化太大，无法在所有地方使用单一机制。

我们可以使用 `Assert::dynamic` 如下：

