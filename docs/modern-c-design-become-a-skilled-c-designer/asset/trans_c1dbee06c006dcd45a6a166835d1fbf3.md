

pdCalc 既有 GUI 也有 CLI，因此添加任何面向用户的功能都需要对两个用户界面组件进行修改。对于存储过程而言，对用户界面的修改非常微小。首先，存储过程只是一个包含 pdCalc 指令有序序列的文本文件。因此，用户可以使用任何纯文本编辑器创建存储过程。因此，除非你想提供一个带语法高亮的存储过程文本编辑器，否则存储过程的用户界面就简化为从 CLI 和 GUI 启用其执行。

让我们先解决在 CLI 中集成存储过程的问题。如前所述，存储过程只是文件系统中的文本文件。回想一下，CLI 通过对空格分隔的输入进行标记化，然后通过引发事件将每个标记单独传递给命令调度器来工作。因此，访问存储过程的一个简单方法是只需将存储过程文件名传递给 CLI。该文件名将像其他命令或数字一样被标记化并传递给命令调度器进行处理。为了确保文件名被命令调度器的解析器解释为存储过程而不是命令，我们只需在文件名前面加上符号 proc: 并更改命令调度器的解析器。例如，对于名为 hypotenuse.psp 的存储过程，我们将向 CLI 发出命令 proc:hypotenuse.psp。我采用文件扩展名 psp 作为 pdCalc 存储过程的缩写。当然，该文件本身是一个普通的 ASCII 文本文件，其中包含用于计算直角三角形斜边的命令序列，如果你愿意也可以使用 .txt 扩展名。

回想一下，GUI 被设计为与 CLI 完全相同的方式将命令传递给命令调度器。因此，为了使用存储过程，我们添加一个按钮以打开对话框来浏览文件系统以查找存储过程。一旦选择了存储过程，我们就在文件名前面加上 proc: 并引发 CommandEntered 事件。

显然，你可以让你的存储过程选择对话框变得尽可能花哨。我选择了一个简化的设计，允许将文件名输入到可编辑的组合框中。为了便于使用，组合框预先填充了当前目录中所有扩展名为 .psp 的文件。

## 8.1.2.2 对命令调度器的更改

清单 8-1 是 CommandDispatcher 的 executeCommand() 函数的简略列表，其中包括解析存储过程所需的逻辑。代码中省略的部分出现在第 4.5.2 节。

CommandDispatcher 的 executeCommand() 函数 清单 8-1。

```
void
CommandDispatcher::executeCommand
string& command)
{

// handle numbers, undo, redo, help in nested
```
```
if
// ...
else if(command.size() > 6 &&
command.substr(0, 5) == "proc:") {

auto filename = command.substr(5,
command.size() - 5); handleCommand(
MakeCommandPtr<StoredProcedure>
(ui_,filename)); }
// else statement to handle Commands from
CommandRepository
// ...

return;
}
```

从上面的代码可以看出，实现只是剥离字符串 command 参数中的 proc: 来创建存储过程文件名，创建一个新的 StoredProcedure 命令子类，并执行此类。现在，我们假设将 StoredProcedure 类作为 Command 类的子类是最佳设计。我将在以下各节中讨论为什么这种策略是首选并检查其实现。然而，在此之前，让我们讨论一下 MakeCommandPtr() 函数的这个新重载。

在第 7.2.1 节中，我们首次看到了由以下实现给出的 MakeCommandPtr 的一个版本：

```
inline void CommandDeleter(Command* p)
{
 p->deallocate(); return;
}
using CommandPtr =
std::unique_ptr<Command,
decltype(&CommandDeleter)>;
inline auto MakeCommandPtr(Command* p)
{
return CommandPtr{p, &CommandDeleter};
}
```

上面的函数是一个帮助函数，用于从原始 Command 指针创建 CommandPtrs。此形式的函数用于从现有 Command 的克隆创建 CommandPtr（例如，如 CommandRepository::allocateCommand() 中所示）：

```
auto p = MakeCommandPtr( command->clone() );
```

在语义上，在 CommandDispatcherImpl::executeCommand( 中我们看到完全不同的用法，即构造一个派生自 Command 的类的实例。当然，我们可以用现有的 MakeCommandPtr 原型满足此用例。例如，我们可以按如下方式创建 StoredProcedure：

```
auto c = MakeCommandPtr(new StoredProcedure{ui,filename});
```

然而，只要有可能，最好不要用裸 new 污染高级代码。因此，我们寻求实现一个重载的帮助函数来为我们执行此构造。它的实现如下所示：

```
template<typename T, typename... Args>
```
```
auto MakeCommandPtr(Args&&... args)
{

return CommandPtr{new
T{std::forward<Args>(args)...},
&CommandDeleter}; }
```

在 C++11 之前，没有简单高效的技术来使用可变数量的构造函数参数构造通用类型，这是创建从 Command 类派生的任何可能类所必需的，每个类都有不同的构造函数参数。然而，现代 C++ 提供了使用可变参数模板和完美转发优雅地解决此问题的解决方案。此构造是下面侧边栏的主题。

## MODERN C++ DESIGN NOTE:
### VARIADIC TEMPLATES AND
### PERFECT FORWARDING

可变参数模板和完美转发在 C++ 中各自解决不同的问题。
可变参数模板使类型安全通用

```
virtual double area() const = 0;
};

class Circle : public Shape
{
public:

Circle(double r) : r_{r} {}
double area() const override { return 3.14159
* r_ * r_; }

private:
double r_;
};

class Rectangle : public Shape
{
public:

Rectangle(double l, double w) : l_{l}, w_{w}
{} double area() const override { return l_ *
w_; } private:
double l_, w_;
};

in C++, substitutability, implemented as
```

虚拟分派，解决了通过基类指针调用派生类型的特定实现的问题，使用基类保证的接口。在形状示例中，可替代性意味着能够按如下方式计算面积：

```
double area(const Shape& s)
{
return s.area();
}
```

对于从 Shape 派生的任何类。虚拟函数的确切接口完全规定，包括任何函数参数的数量和类型（即使在 area() 函数的此示例中空虚的情况下）。问题是，对象构造永远无法以这种方式“虚拟化”，即使可以，也不会起作用，因为构造对象所需的信息（其参数）非常频繁地从一个派生类到下一个派生类不同。

进入通用完美转发
构造函数模式。在此模式中，我们使用可变参数模板提供一个类型安全的接口，可以采用任意数量具有不同类型的构造函数参数。第一个模板参数始终是我们想要构造的类型。然后，使用完美转发来保证参数以正确的类型传递给构造函数。完美转发在此情况下为何必要的确切原因源于模板中类型的推导方式，超出了本讨论的范围（详见 [19]）。对于我们的形状示例，应用 GpFC 模式得到以下实现：

```
template<typename T, typename... Args>
auto MakeShape(Args&&... args)
{

return make_unique<T>(forward<Args>
(args)...); }
```

下面的代码说明了如何使用 MakeShape() 函数创建具有不同数量构造函数参数的不同类型：

```
auto c = MakeShape<Circle>(4.0);  
auto r = MakeShape<Rectangle>(3.0, 5.0);
```

请注意，GpFC 模式也适用于创建彼此之间没有继承层次关系的类。事实上，GpFC 模式被标准库中的 make_unique() 函数用于以高效、通用且不需要裸 new 的方式创建 unique_ptrs。虽然严格来说它们是不同的，但我喜欢将 GpFC 模式视为工厂方法的通用类似物。

## 8.1.2.3 设计存储过程类

我们现在回到设计 StoredProcedure 类的棘手问题。我们首先问的问题是我们是否需要一个类。我们已经有了一个用于解析单个命令、执行它们并将它们放在撤销/重做堆栈上的设计。也许正确的答案是以与

