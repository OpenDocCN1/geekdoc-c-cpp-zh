
其中一个属性变更方法的实现示例是，通过抛出异常来拒绝无效输入。另一个用途则是在发生更改时执行某种日志记录。分部方法特性最关键的地方在于，它将生成的代码与可自定义的代码清晰地分离开来，而这两类代码都属于同一个类型定义：

```
partial class Person
{
    partial void OnAgeChanging(int value)
    {
        if (value <= 0)
            throw new ArgumentOutOfRangeException("value");
    }

    partial void OnCreated()
    {
        Console.WriteLine("New Person created.");
    }
}
```

当分部方法没有给出实现时，整个调用点（通常在类定义中由生成代码产生的部分）就会直接消失。例如，对于前面的代码，`Age` 的设置器实际看起来会像这样：

```
if ((this._Age != value)) {
    this.OnAgeChanging(value);
    this.SendPropertyChanging();
    this._Age = value;
    this.SendPropertyChanged("Age");
    // This code gets dropped as no implementation is given:
    // this.OnAgeChanged();
}
```

使用 Reflector 或 ILDASM 之类的工具很容易验证这一说法。由于这种技术，分部方法只能返回 `void`，并且不能有任何输出参数。如果不是这样，那么在没有给出实现的情况下，方法调用产生的那些输出值将无从确定。

此外，分部方法只能是私有的（因此不允许使用任何访问修饰符）。如果它们是公共的，并且有人试图在无法保证实现存在的情况下调用它们，就会发生严重问题。同样，委托也不可能引用分部方法，因为它可能不存在。

总之，分部方法的使用通常与代码生成场景相关，在这种情况下，代码生成器希望向开发人员提供“扩展点”。通过这种方式，可以在自定义逻辑和生成代码之间实现清晰的分离。在运行时层面，并没有分部类或分部方法这种东西；它们纯粹是编译时的幻象。

## 外部方法

C# 支持的另一种方法声明类型是外部方法。基本上，它可以让你指定一个定义在别处的方法。这听起来相当含糊，事实也确实如此，因为运行时必须介入并帮助找到该方法的实际实现。基本上，对最终用户而言唯一直接适用的场景是 P/Invoke 技术，即桥接到非托管代码中定义的方法（例如 Win32 API 中的方法）。下面的代码展示了它的实际用法：

```
public static void Main(string[] args)
{
    int size = 0;
    var user = new StringBuilder(size);
    if (!GetUserName(user, ref size))
    {
        var error = Marshal.GetLastWin32Error();
        if (error != ERROR_INSUFFICIENT_BUFFER)
        {
            Console.WriteLine("Unexpected error: " + error);
            return;
        }
    }

    user = new StringBuilder(size);
    if (!GetUserName(user, ref size))
    {
        var error = Marshal.GetLastWin32Error();
        Console.WriteLine("Unexpected error: " + error);
        return;
    }

    Console.WriteLine("Welcome, {0}", user.ToString());
}

const int ERROR_INSUFFICIENT_BUFFER = 122;

[DllImport("Advapi32.dll", SetLastError = true)]
static extern bool GetUserName(StringBuilder lpBuffer, ref int nSize);
```

互操作管线可能相当具有挑战性，因为你需要处理很多事情。其中一个关键点是确保互操作签名在数据类型以及参数的输入/输出行为方面是正确的。www.pinvoke.net 社区网站可以帮助你找到 Win32 API 的互操作签名，事实上这里展示的 `DllImport` 就取自该网站。

虽然我们本可以一开始就分配一个足够大的缓冲区（在 Windows 7 中，用户名的当前最大长度被设置为 256，该值在 SDK 中 `LMCons.h` 头文件里的 `UNLEN` `#define` 中定义），但我们采用了一种更能说明在处理 P/Invoke 时典型且过度的错误检查和处理方式的编码方法。应用于外部方法的 `DllImport` 特性上的参数指明了函数定义的位置以及其行为的某些方面，例如错误代码通信和字符串封送（在非托管世界中有很多不同种类的字符串）。这里我们使用的 `GetUserName` 函数定义在 `Advapi32.dll` Win32 系统二进制文件中。其签名与本机函数的签名一致（更多信息请参阅 MSDN）：

```
[DllImport("Advapi32.dll", SetLastError = true)]
static extern bool GetUserName(StringBuilder lpBuffer, ref int nSize);
```

`SetLastError` 的使用表明该函数是否使用 Win32 的 `GetLastError` 方式来存储错误代码。本质上，这告诉 CLR 的互操作基础设施在 P/Invoke 调用返回时调用 `GetLastError`，这样托管代码就可以通过 `Marshal.GetLastWin32Error` 访问最后的 Win32 错误代码（这是另一组在 MSDN 文档中记录的晦涩常量）。

从语言角度来看，外部方法使用 `extern` 关键字表示，不能有实现体（注意必须带有结尾分号），并且必须应用一个自定义特性。从运行时的角度来看，方法如何被找到取决于应用于该方法的特性。`DllImport` 就是运行时知道的一种此类特性，它会在需要调度方法调用时触发并接入 P/Invoke 基础设施。

还存在其他用于外部方法的特性，但它们不能直接被框架用户访问。一个例子是 `MethodImpl`，它可以用于对运行时基础设施方法进行内部调用。例如 `System.Object.GetType` 方法，其实现深藏在运行时内部。图 10.20 通过 Reflector 展示了其定义上使用 `extern` 修饰符的情况。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_567_0.png)

图 10.20 用于 Object 上外部 `GetType` 方法的内部运行时调用。

## 重构

重构是适用于一系列技术的标签，这些技术涉及持续关注以保持程序代码的可读性、可维护性和健全性，以便于未来扩展。实现这一目标的一种方法是降低系统中不同部件或组件的复杂性和纠缠程度。虽然方法和代码的其他操作方面是重构的典型目标，但类似的技术也适用于程序中数据密集的部分。例如，虽然让一个 `Person` 对象包含街道、城市和邮政编码可能是有意义的，但与某个在线地图服务的集成可能会引导我们采用一种设计，即 `Person` 拥有一个 `Address` 对象。

可以使用各种指标来量化一段代码的复杂性和可维护性。优秀的开发人员往往会在自动驾驶状态下操作时识别出重构的需要，不过各种工具也可以帮助发现潜在的代码维护噩梦。Visual Studio 有一个代码度量功能，可以帮助发现可能的问题，如图 10.21 和图 10.22 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_567_1.png)

图 10.21 计算项目的代码度量。

