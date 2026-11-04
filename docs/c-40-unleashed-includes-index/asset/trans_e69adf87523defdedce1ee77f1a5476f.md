
- **Source（源）** 可以设置，用于标识异常来自何处（例如，使用应用程序组件或对象的标识符）。如果未设置，则使用引发异常时所在程序集的名称。
- **StackTrace（堆栈跟踪）** 包含引发异常时的调用堆栈，并且即使故障发生时没有附加调试器，也可用于调试错误状况。在提供符号文件的调试版本中，还可能显示诸如行号之类的附加信息。
- **TargetSite（目标站点）** 提供反射 `MethodBase` 对象，指示引发异常的位置。

定义自己的异常类型时，至少应提供有意义的 `Message` 属性，并在合理时提供 `InnerException`。此外，序列化支持非常可取。

为了帮助开发者编写符合这些要求的正确异常类型，Visual Studio 中提供了一个代码片段来生成可自定义的模板代码。这个代码片段称为 Exception，像所有代码片段一样，可以通过键入其名称然后按两次 Tab 键来插入（见图 23.14）。

```csharp
namespace Exceptions
{
    [global::System.Serializable]
    public class MyException : Exception
    {
        public MyException() { }
        public MyException(string message) : base(message) { }
        public MyException(string message, Exception inner) : base(message, inner) { }
        protected MyException(
            System.Runtime.Serialization.SerializationInfo info,
            System.Runtime.Serialization.StreamingContext context)
            : base(info, context) { }
    }
}
```

**图 23.14** 展开后的 Exception 代码片段。

可自定义的点包括异常名称（作为常见后缀 Exception 的前缀）以及基类。注意，通过 Serializable 特性和受保护构造函数，如何开箱即用地提供序列化支持。有关序列化的更多信息，请查看 MSDN 文档，可以从 System.Exception 基类开始查找。

## 编写优秀代码片段的关键

优秀的代码片段只要插入到合适的位置，就能正常工作。Exception 代码片段显然在设计时考虑了这一准则：命名空间被完全展开，并使用 global 关键字确保从全局命名空间中找到 Serializable 自定义特性。不幸的是，这会增加杂乱内容，而这些内容在插入代码片段的上下文中往往无关紧要。我通常会清理代码片段插入所生成的代码。只要安全，就可以随时这样做（例如，如果没有命名空间冲突）。

自定义异常类型有多种价值。在定位适用的 catch 块时，基于类型的匹配不仅提供了进行细粒度异常处理的理想方式，还使你能够随着时间的推移演进异常类型，例如通过为它们添加更多属性，甚至引入新的子类型。稍后我们会更仔细地了解各种可复用的内置异常类型，但如果你要描述特定于应用程序或库的错误状况，定义自己的自定义异常类型被视为最佳实践。

## 来自实战的过度设计：ApplicationException

当异常最初被设计时，人们认为为 CLR 异常和应用程序定义的异常引入单独的类层次结构是个好主意。这促成了两个从 Exception 派生的类的定义。一个称为 SystemException，保留给 CLR 和核心框架组件用来指示错误状况。另一个称为 ApplicationException，原本旨在作为应用程序定义的异常的基类。

这个出于好意的想法最终并没有增加多少价值，而且由于并未阻止直接从 Exception 派生，许多应用程序和框架开始将其作为首选基类。它很快变成了一条设计准则：直接从 Exception 派生，忘掉 ApplicationException。因此，代码片段直接从 Exception 派生是正确的。

## （不）著名的异常类型

基类库（BCL）预定义了许多异常类型。现在我们来看一些每个人都应该了解的最重要的异常类型（不仅要准备好在适当的时候处理其中任何一种，还要在应用程序应当直接使用它们时抛出它们）。

### DivideByZeroException

当对整型或十进制值执行除以零的操作时，就会发生此异常；应用程序可以通过预先检查分母是否为零来避免它。回想一下，浮点类型定义了无穷大和非数字（NaN）值，这些值将用于除以零尝试的结果。

这里的第二行和第三行会引发此异常，无论是否使用检查上下文；其他整型和十进制数据类型也是如此：

```
int n = 1, d = 0;
int div = n / d;
int rem = n % d;
```

### OverflowException

仍然在算术领域，我们会遇到 OverflowException；每当算术运算、强制转换或转换在检查上下文中溢出时，就会发生此异常。有关检查上下文的更多信息，请参见第 5 章“表达式”。

使用检查上下文的目的是使应用程序在面对会产生错误结果的溢出情况时更加健壮。默认情况下，C# 程序以未检查的算术、强制转换和转换操作进行编译。Visual Basic 反转了这一默认设置，这可能会对性能产生负面影响。

在预期不会发生溢出的情况下，不处理这种异常类型并不少见，但仍然会使用检查上下文，以防万一发生溢出时防止产生错误结果。这在金融或科学计算中很典型，不过也常常完全使用不同的类型（如 BigInteger）来消除对数值精度和范围的限制。

下面展示几个溢出示例：

```
checked {
    int tooHigh = int.MaxValue + 1; // add.ovf
    int tooLow = int.MinValue - 1;  // sub.ovf
    byte b = 200;
    sbyte s = (sbyte)b;             // conv.ovf
}
```

### NullReferenceException

对于来自原生代码领域的人来说，NullReferenceException 就是托管世界中现代版的访问冲突对应物。如果你的背景在其他领域，只需记住，这种异常是你在代码中永远不想看到的。

糟糕的是，引用类型默认允许空引用，这使得该异常在测试不充分的代码中极为常见。未能返回合适的对象时，常常通过空引用来表示，这给调用方提供了绝佳的自找麻烦的机会——只要省略空检查即可。所以，不要让自己掉进这个陷阱。相反，应在必要时检查空值：

```
string s = GetStringMaybeNull();
string oops = s.ToUpper();
```

NullReferenceException 错误的另一个常见来源，是在更适合使用常规强制转换的地方不恰当地使用了 as 关键字：

```
object o = GetSomeObject();
string s = o as string;     // No null check? Cast!
string oops = s.ToUpper();
```

如果你知道 o 应该是 string，请使用常规强制转换，而不是 as 表达式。这将导致 InvalidCastException，它能让你更好地了解出了什么问题。在其他确实合理使用 as 关键字的情况下，你应该会看到用空检查来检查操作结果。

在表达式上下文中，处理空引用的方式有多种，如前所述。一种是空合并 ?? 运算符，它使你能够提供一个默认值来替代空引用；另一种是使用条件运算符，并以空检查作为条件：

```
string s = GetStringMaybeNull();
string okay = s ?? "(empty)";
string fine = s != null ? s.ToUpper() : "(empty)";
```

计算机科学家 Tony Hoare 最近把 ALGOL 中引入空引用（早在 1965 年）称为“他的十亿美元错误”。别让它们找上你！

### IndexOutOfRangeException

另一类会暴露低级错误的异常是 IndexOutOfRangeException，它表示数组被访问时超出了边界。“差一”错误是这种异常的典型来源：

```
int[] nums = new[] { 1, 2, 3 };
for (int i = 0; i <= nums.Length; i++)
    nums[i]++;
```

边界检查历来是缺陷的来源，这些缺陷在原生代码世界中常常未被注意到，并因内存损坏而导致程序随机崩溃。你应该感到幸运，CLR 使用运行时检查捕获了这类问题（以避免其内存和类型安全受到破坏），但首先就不要写出这样的缺陷！差一错误可能很隐蔽，但只要多思考一点，你应该就能避免再次看到这种异常。

### InvalidCastException

能够将对象强制转换为不兼容的类型，会破坏系统的类型安全，而这显然应当避免。InvalidCastException 是 CLR 阻止所有此类尝试的方式。

如今，在引入泛型类型之后，强制转换的使用应该已经比过去少得多了。每次你必须将对象强制转换为更具体的类型时，问问自己最初是怎么陷入这种局面的。也许这与泛型有关。如果你发现自己使用 is 或 as 执行基于类型的 switch，也许使用面向对象的虚拟分派机制更合适。

