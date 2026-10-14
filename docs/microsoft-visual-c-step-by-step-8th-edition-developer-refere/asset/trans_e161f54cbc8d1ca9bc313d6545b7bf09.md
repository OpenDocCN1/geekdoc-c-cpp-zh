

并且有一个名为 answer 的单个 int 参数：

```
void showResult(int answer)
{
    // ...
}
```

注意使用关键字 void 来表示该方法不返回任何内容。

## Important

如果你熟悉 Visual Basic，请注意 C# 不使用不同的关键字来区分返回值的 方法（函数）和不返回值的方法（过程或子程序）。你必须始终指定返回类型或 void。

## Returning data from a method

如果你希望方法返回信息（即其返回类型不是 void），则必须在方法体中处理的末尾包含 return 语句。return 语句由关键字 return、指定返回值的表达式以及分号组成。表达式的类型必须与方法声明中指定的类型相同。例如，如果方法返回 int，则 return 语句必须返回 int；否则，你的程序将无法编译。以下是带 return 语句的方法示例：

Click here to view code image

```
int addValues(int leftHandSide, int rightHandSide)
{
    // ...
    return leftHandSide + rightHandSide;
}
```

return 语句通常位于方法的末尾，因为它会导致方法结束，并且控制权返回到调用该方法的语句，如本章后面所述。return 语句之后出现的任何语句都不会被执行（尽管如果在 return 语句之后放置语句，编译器会警告你这个问题）。

如果你不希望方法返回信息（即其返回类型为 void），可以使用 return 语句的变体来立即退出方法。你写下关键字 return 并立即跟上分号。例如：

Click here to view code image

```
void showResult(int answer)
{
    // display the answer
    Console.WriteLine($"The answer is {answer}");
    return;
}
```

如果你的方法不返回任何内容，你也可以省略 return 语句，因为当执行到达方法末尾的闭合大括号时，方法会自动结束。虽然这种做法很常见，但并不总是被认为是一种好的风格。

## Using expression-bodied methods

一些方法可以非常简单，只执行单一任务或返回计算结果，而不涉及任何额外逻辑。C# 支持一种简化形式，用于由单个表达式组成的方法。这些方法仍然可以接受参数并返回值，并且它们的工作方式与迄今为止看到的方法相同。以下代码示例显示了作为表达式体方法编写的 addValues 和 showResult 方法的简化版本：

Click here to view code image

```
int addValues(int leftHandSide, int rightHandSide) => leftHandSide + rightHandSide;

void showResult(int answer) => Console.WriteLine($"The answer is {answer}");
```

主要区别在于使用 => 运算符引用构成方法体的表达式，以及没有 return 语句。表达式的值用作返回值；如果表达式不返回值，则方法为 void。

实际上，使用普通方法和表达式体方法之间在功能上没有任何区别——表达式体方法只是语法上的便利。然而，你将在本书后面的示例中看到，表达式体方法可以通过删除大量多余的 { 和 } 字符来阐明程序，使代码更易于阅读。

在下面的练习中，你将检查第 2 章中 MathsOperators 项目的另一个版本。此版本通过仔细使用一些小方法而得到改进。以这种方式划分代码有助于使其更易于理解和维护。

## Examine method definitions

- 1. 如果尚未运行，请启动 Visual Studio 2015。
- 2. 打开 Methods 项目，该项目位于你的 Documents 文件夹中的 \Microsoft Press\VCSBS\Chapter 3\Methods 文件夹中。
- 3. 在 Debug 菜单上，单击 Start Debugging。
- 4. Visual Studio 2015 构建并运行应用程序。它应该看起来与第 2 章中的应用程序相同。重新熟悉应用程序及其工作原理，然后返回 Visual Studio。在 Debug 菜单上，单击 Stop Debugging。
- 5. 在代码和文本编辑器窗口中显示 MainPage.xaml.cs 的代码（在 Solution Explorer 中，展开 MainPage.xaml 文件，然后双击 MainPage.xaml.cs）。
- 6. 在代码和文本编辑器窗口中，找到 *addValues* 方法，它看起来像这样：

Click here to view code image

```
private int addValues(int leftHandSide, int rightHandSide)
{
    expression.Text = $"{leftHandSide} + {rightHandSide}";
    return leftHandSide + rightHandSide;
}
```

### Note

暂时不用担心此方法定义开头的 *private* 关键字；你将在第 7 章“创建和管理类和对象”中学习此关键字的含义。

*addValues* 方法包含两个语句。第一个语句在表单上的 *expression* 框中显示正在执行的计算。

第二个语句使用 *int* 版本的 + 运算符将 *leftHandSide* 和 *rightHandSide int* 变量的值相加，然后返回此操作的结果。请记住，将两个 *int* 值相加会产生另一个 *int* 值，因此 *addValues* 方法的返回类型为 *int*。

如果你查看 *subtractValues*、*multiplyValues*、*divideValues* 和 *remainderValues* 方法，你会发现它们遵循类似的模式。

7. 在代码和文本编辑器窗口中，找到 *showResult* 方法，它看起来像这样：

Click here to view code image

```
private void showResult(int answer) => result.Text = answer.ToString();
```

这是一个表达式体方法，它在 *result* 框中显示 *answer* 参数的字符串表示形式。它不返回值，因此此方法的类型为 *void*。

### Tip

方法没有最小长度。如果方法有助于避免重复并使你的程序更易于理解，无论它有多小，该方法都是有用的。

方法也没有最大长度，但通常你希望保持方法代码足够小以完成任务。如果你的方法长度超过一屏，请考虑将其拆分为更小的方法以提高可读性。

## Calling methods

方法存在的意义就是被调用！你通过名称调用方法来要求它执行其任务。如果方法需要信息（按其参数指定），你必须提供所需的信息。如果方法返回信息（按其返回类型指定），你应该安排以某种方式捕获此信息。

### Specifying the method call syntax

C# 方法调用的语法如下：

Click here to view code image

```
result = methodName ( argumentList )
```

以下是构成方法调用的元素的描述：

- *methodName* 必须与你要调用的方法的名称完全匹配。请记住，C# 是区分大小写的语言。
- *result =* 子句是可选的。如果指定，则变量 *result* 包含方法返回的值。如果方法为 *void*（即不返回值），你必须省略语句的 *result =* 子句。如果方法确实返回值但你未指定 *result =* 子句，方法仍会运行但返回值将被丢弃。
- *argumentList* 提供方法接受的信息。你必须为每个参数提供一个参数，并且每个参数的值必须与其对应参数的类型兼容。如果你要调用的方法有两个或多个参数，你必须用逗号分隔参数。

## Important

你必须在每次方法调用中包含括号，即使调用一个没有参数的方法时也是如此。

