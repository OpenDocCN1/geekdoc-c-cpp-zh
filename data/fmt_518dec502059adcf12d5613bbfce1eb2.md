
- c. 调用 `Pass.Reference` 方法，将 `wi` 作为参数传递。

- d. 再次将 `wi.Number` 的值写入控制台。

与之前一样，通过 `Console.WriteLine` 的调用，你可以看到调用 `Pass.Reference` 是否修改了 `wi.Number` 的值。`doWork` 方法现在应完全如下所示（新语句以粗体突出显示）：

Click here to view code image

```
static void doWork()
{
    // int i = 0;
    // Console.WriteLine(i);
    // Pass.Value(i);
    // Console.WriteLine(i);

    WrappedInt wi = new WrappedInt();
    Console.WriteLine(wi.Number);
    Pass.Reference(wi);
    Console.WriteLine(wi.Number);
}
```

### 14. 在 Debug 菜单上，单击 Start Without Debugging 以构建并运行应用程序。

这次，控制台窗口中显示的两个值对应于调用 `Pass.Reference` 方法之前和之后 `wi.Number` 的值。你应该会看到显示值 0 和 42。

### 15. 按 Enter 键关闭应用程序并返回到 Visual Studio 2015。

要解释之前的练习显示的内容，`wi.Number` 的值由编译器生成的默认构造函数初始化为 0。`wi` 变量包含对新创建的 `WrappedInt` 对象（其中包含一个 `int`）的引用。然后 `wi` 变量作为参数复制到 `Pass.Reference` 方法。因为 `WrappedInt` 是一个类（引用类型），`wi` 和 `param` 都引用同一个 `WrappedInt` 对象。通过 `Pass.Reference` 方法中的 `param` 变量对对象内容所做的任何更改，都可以通过方法完成时使用 `wi` 变量来看到。下面的图表说明了将 `WrappedInt` 对象作为参数传递给 `Pass.Reference` 方法时会发生什么：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_236_0.png)

## 理解 null 值和可空类型

当你声明一个变量时，始终最好对其进行初始化。对于值类型，常见的代码如下：

```
int i = 0;
double d = 0.0;
```

记住，要初始化诸如类之类的引用变量，你可以创建类的一个新实例并将引用变量分配给新对象，如下所示：

```
Circle c = new Circle(42);
```

这都很好，但如果实际上你并不想创建新对象怎么办？也许变量的目的是在程序的稍后阶段简单地存储对现有对象的引用。在以下代码示例中，`Circle` 变量 `copy` 被初始化，但后来它被分配了对 `Circle` 类的另一个实例的引用：

Click here to view code image

```
Circle c = new Circle(42);
Circle copy = new Circle(99);  // Some random value, for
initializing copy
...
copy = c;                  // copy and c refer to the same
object
```

将 `c` 分配给 `copy` 后，你用来初始化 `copy` 的半径为 99 的原始 `Circle` 对象会发生什么？没有任何东西再引用它了。在此 situation，运行时可以通过执行称为 *垃圾回收* 的操作来回收内存，你将在第 14 章“使用垃圾回收和资源管理”中了解更多相关内容。现在需要理解的重要一点是，垃圾回收是一个可能耗时的操作；你不应该创建永远不会使用的对象，因为这样做会浪费时间和资源。

你可以争辩说，如果程序中某个变量最终会被赋值为另一个对象的引用，那么初始化它就没有意义了。但这是一种糟糕的编程实践，可能会导致代码出现问题。例如，你不可避免地会遇到想要仅在该变量尚未包含引用时才将变量引用到一个对象的情况，如以下代码示例所示：

Click here to view code image

```
Circle c = new Circle(42);
Circle copy;                  // Uninitialized !!!
...
if (copy == // only assign to copy if it is uninitialized, but what goes here?)
{
    copy = c;                  // copy and c refer to the same object
    ...
}
```

*if* 语句的目的是测试 *copy* 变量是否已初始化，但你应该将此变量与哪个值进行比较？答案是使用一个特殊值 *null*。

在 C# 中，你可以将 *null* 值赋给任何引用变量。*null* 值仅表示该变量不引用内存中的对象。你可以这样使用它：

Click here to view code image

```
Circle c = new Circle(42);
Circle copy = null;          // Initialized
...
if (copy == null)
{
    copy = c;                  // copy and c refer to the same object
    ...
}
```

## Null-conditional operators

最新版本的 C# 包含一个新运算符，即 null 条件运算符，它使你能够更简洁地测试 null 值。要使用 null 条件运算符，你只需在变量名称后附加一个问号（?）。

例如，假设你尝试在 `Circle` 对象具有 `null` 值时调用 `Circle` 对象的 `Area` 方法：

Click here to view code image

```
Circle c = null;
Console.WriteLine($"The area of circle c is {c.Area()}");
```

在这种情况下，`Circle.Area` 方法会抛出 `NullReferenceException`，这是有意义的，因为你无法计算不存在的圆的面积。

为了避免此异常，你可以在尝试调用 `Circle.Area` 方法之前先测试 `Circle` 对象是否为空：

Click here to view code image

```
if (c != null)
{
    Console.WriteLine($"The area of circle c is {c.Area()}");
}
```

在这种情况下，如果 `c` 为 `null`，则不会向命令窗口写入任何内容。或者，你也可以在尝试调用 `Circle.Area` 方法之前对 `Circle` 对象使用 null 条件运算符：

Click here to view code image

```
Console.WriteLine($"The area of circle c is {c?.Area()}");
```

null 条件运算符告诉运行时引擎，如果你对该运算符应用的变量为 `null`，则忽略当前语句。在这种情况下，命令窗口将显示以下文本：

```
The area of circle c is
```

这两种方法都是有效的，并且可能在不同场景下满足你的需求。null 条件运算符可以帮助你使代码更简洁，特别是当你处理包含可能全部为 `null` 值的嵌套引用类型的复杂属性时。

## Using nullable types

`null` 值对于初始化引用类型很有用。有时，你需要为值类型提供等效值，但 `null` 本身是一个引用，因此你无法将其赋给值类型。因此，以下语句在 C# 中是非法的：

```
int i = null; // illegal
```

然而，C# 定义了一个修饰符，你可以使用它来声明变量为 *nullable* 值类型。nullable 值类型与原始值类型以类似的方式表现，但你可以为其赋 *null* 值。你使用问号（?）来指示值类型为 nullable，如下所示：

```
int? i = null; // legal
```

你可以通过与测试引用类型相同的方式来确定 nullable 变量是否包含 *null*。

```
if (i == null)
    ...
```

你可以将适当值类型的表达式直接赋给 nullable 变量。以下示例都是合法的：

Click here to view code image

```
int? i = null;
int j = 99;
i = 100;      // Copy a value type constant to a nullable type
i = j;        // Copy a value type variable to a nullable type
```

你应该注意，反过来是不成立的。你不能将 nullable 变量赋给普通值类型变量。因此，给定前一个示例中变量 *i* 和 *j* 的定义，以下语句是不允许的：

```
j = i;      // Illegal
```

当你考虑到变量 *i* 可能包含 *null*，而 *j* 是不能包含 *null* 的值类型时，这是有意义的。这也意味着你不能将 nullable 变量用作期望普通值类型的方法的参数。如果回忆一下，前一个练习中的 *Pass.Value* 方法期望一个普通的 *int* 参数，因此以下方法调用将无法编译：

Click here to view code image

```
int? i = 99;
Pass.Value(i);    // Compiler error
```

### Note

请注意不要将 nullable 类型与 null 条件运算符混淆。nullable 类型是通过在类型名称后附加问号来表示的，而 null 条件运算符则是附加到变量名称上。

## Understanding the properties of nullable types

nullable 类型公开了一对属性，你可以使用它们来确定该类型是否实际具有非 null 值以及该值是什么。`HasValue` 属性指示 nullable 类型是否包含值或为 `null`。你可以通过读取 `Value` 属性来检索非 null nullable 类型的值，如下所示：

Click here to view code image

```
int? i = null;
...
if (!i.HasValue)
{
    // If i is null, then assign it the value 99
    i = 99;
}
else
{
    // If i is not null, then display its value
    Console.WriteLine(i.Value);
}
```

第 4 章“使用决策语句”说明 NOT 运算符（!）否定布尔值。此代码片段测试 nullable 变量 `i`，如果它没有值（为 `null`），则将其赋值为 99；否则，它会显示变量的值。在此示例中，使用 `HasValue` 属性与直接测试 `null` 值相比并无任何好处。此外，读取 `Value` 属性是读取变量内容的一种冗长方式。然而，这些明显的不足是由 `int?` 是一个非常简单的 nullable 类型这一事实造成的。你可以创建更复杂的值类型并使用它们声明 nullable 变量，在这种情况下使用 `HasValue` 和 `Value` 属性的优势会变得更加明显。你将在第 9 章“使用枚举和结构创建值类型”中看到一些示例。

### Note

nullable 类型的 `Value` 属性是只读的。你可以使用此属性读取变量的值，但不能修改它。要更新 nullable 变量，请使用普通的赋值语句。

## Using ref and out parameters

通常，当你向方法传递参数时，对应的参数会被参数的副本初始化。这无论参数是值类型（如 `int`）、nullable 类型（如 `int?`）还是引用类型（如 `WrappedInt`）都成立。这种安排意味着参数的任何更改都不会影响传入参数的值。例如，在以下代码中，输出到控制台的值是 42，而不是 43。*doIncrement* 方法递增的是参数（*arg*）的 *副本*，而不是原始参数，如下所示：

Click here to view code image

```
static void doIncrement(int param)
{
    param++;
}

static void Main()
{
    int arg = 42;
    doIncrement(arg);
    Console.WriteLine(arg); // writes 42, not 43
}
```

在前一个练习中，你看到如果方法的参数是引用类型，使用该参数所做的任何更改都会更改传入参数所引用的数据。关键点是：虽然引用的数据发生了更改，但作为参数传入的参数本身并未更改——它仍然引用同一个对象。换句话说，虽然可以通过参数修改参数所引用的对象，但无法修改参数本身（例如，使其引用完全不同的对象）。大多数情况下，这种保证非常有用，可以帮助减少程序中的错误。然而，有时你可能希望编写一个实际上需要修改参数的方法。C# 提供了 *ref* 和 *out* 关键字，使你能够做到这一点。

## Creating *ref* parameters

如果你在参数前加上 *ref* 关键字，C# 编译器会生成将实际参数的引用而非参数的副本传递的代码。使用 *ref* 参数时，对参数所做的任何操作也会对原始参数执行，因为参数和参数都引用相同的数据。当你将参数作为 *ref* 参数传递时，你还必须在参数前加上 *ref* 关键字。这种语法为程序员提供了有用的视觉提示，表明参数可能会发生变化。以下是前一个示例的修改版本，使用了 *ref* 关键字：

Click here to view code image

```
static void doIncrement(ref int param) // using ref
{
    param++;
}

static void Main()
```

```
{
    int arg = 42;
    doIncrement(ref arg);    // using ref
    Console.WriteLine(arg);  // writes 43
}
```

这次，`doIncrement` 方法接收的是原始参数的引用而不是副本，因此方法通过此引用所做的任何更改都会实际改变原始值。这就是为什么控制台上显示的值为 43。

请记住，C# 强制执行必须在读取变量之前为其赋值这一规则。此规则也适用于方法参数；即使参数定义为 `ref` 参数，你也不能将未初始化的值作为参数传递给方法。例如，在下面的示例中，`arg` 未初始化，因此此代码无法编译。此失败的原因是 `doIncrement` 方法中的语句 `param++;` 实际上是 `arg++;` 的别名——而此操作仅在 `arg` 具有已定义值时才允许：

Click here to view code image

```
static void doIncrement(ref int param)
{
    param++;
}

static void Main()
{
    int arg;            // not initialized
    doIncrement(ref arg);
    Console.WriteLine(arg);
}
```

## Creating out parameters

编译器会检查在调用方法之前 `ref` 参数是否已被赋值。然而，可能存在你希望方法本身初始化参数的情况。你可以使用 `out` 关键字来实现这一点。

`out` 关键字在语法上与 `ref` 关键字相似。你可以用 `out` 关键字作为前缀来修饰一个参数，使其成为参数的别名。与使用 `ref` 时一样，对参数所做的任何操作也会对原始参数执行。当你将参数传递给 `out` 参数时，也必须用 `out` 关键字作为前缀。

关键字 `out` 是 `output` 的缩写。当你将 `out` 参数传递给方法时，该方法必须在完成或返回之前为其赋值，如以下示例所示：

Click here to view code image

```
static void doInitialize(out int param)
{
```

```
param = 42; // Initialize param before finishing
}
```

下面的示例无法编译，因为 `doInitialize` 没有为 `param` 赋值：

Click here to view code image

```
static void doInitialize(out int param)
{
    // Do nothing
}
```

由于 `out` 参数必须由方法赋值，因此允许你在不初始化其参数的情况下调用该方法。例如，下面的代码调用 `doInitialize` 来初始化变量 `arg`，然后将其显示在控制台上：

Click here to view code image

```
static void doInitialize(out int param)
{
    param = 42;
}

static void Main()
{
    int arg;                // not initialized
    doInitialize(out arg);  // legal
    Console.WriteLine(arg); // writes 42
}
```

你将在下一个练习中检查 `ref` 参数。

## Use ref parameters

+   1. Return to the Parameters project in Visual Studio 2015.

+   2. Display the Pass.cs file in the Code and Text Editor window.
