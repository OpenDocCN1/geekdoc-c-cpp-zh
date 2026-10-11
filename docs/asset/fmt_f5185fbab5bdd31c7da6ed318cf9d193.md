
((Angle)objectAngle).MoveTo(26, 58, 23);

Console.Write("" + ((Angle)objectAngle).Degrees);

```csharp
// 示例 3：装箱、修改装箱后的值
// 并丢弃引用
((IAngle)angle).MoveTo(26, 58, 23);
Console.Write("" + ((Angle)angle).Degrees);
```

```csharp
// 示例 4：直接修改装箱值
((IAngle)objectAngle).MoveTo(26, 58, 23);
Console.WriteLine("" + ((Angle)objectAngle).Degrees);
```

```text
{
  ...
}
```

# OUTPUT 9.2

```
25, 25, 25, 26
```

列表 9.11 使用了 `Angle` 结构体和 `IAngle` 接口。注意 `IAngle.MoveTo()` 接口使 `Angle` 变为可变。这种变化突出了可变值类型的特殊之处，并此演示了提倡使结构体不可变的准则的重要性。

在列表 9.11 的示例 1 中，在初始化 `angle` 后，变量 `objectAngle` 没有发生变化。接下来，示例 2 调用 `MoveTo()` 将 `_Degrees` 修改为 26。然而，如输出所示，第一次并没有发生变化。问题在于调用 `MoveTo()`，编译器拆箱了 `objectAngle` 并（根据定义）创建了值的副本。值类型按值传递的——这就是为什么它们被称为值类型。尽管结果值在执行时被成功修改了，但这个值的副本被丢弃了，`objectAngle` 所引用的堆位置没有发生变化。

# 第 9 章：引入结构体和记录

回顾我们之前的类比：值类型的建议变量就像写有值的纸条。当你对一个值进行装箱（boxing）时，你对这张纸条进行了复印，并将副本放在盒子里。当你拆箱（unboxing）该值时，你对盒子里的纸条进行了复印。对这第二个副本进行编辑不会改变盒子中的那个副本。

在示例 3 中，发生了类似的问题，但方向相反。程序没有直接调用 `MoveTo()`，而是将值转换为 `IAngle`。转换为接口会对值进行装箱，因此运行时会将 `angle` 中的数据拷贝到堆上，并提供指向该箱的引用。接下来，方法调用修改了被引用箱中的值。变量 `angle` 中存储的值保持未修改。

在最后一种情况下，转换为 `IAngle` 是引用转换，而不是装箱转换。在这种情况下，值已经被 `object` 装箱了，因此在转换过程中没有发生值的拷贝。对 `MoveTo()` 的调用更新了箱中存储的值，代码行为符合预期。

正如你从这个示例看到的，可变值类型非常令人困惑，因为通常不清楚你是在修改值的副本还是修改你实际想要更改的存储位置。通过从源上避免可变值类型，你可以消除这种困惑。

> 指南
避免使用可变值类型。

## 高级主题：在方法调用期间避免装箱

### 如何在方法调用期间避免装箱
每当在值类型上调用方法时，接收调用的值类型（在方法体内用 `this` 表示）必须是一个变量而不是一个值，因为方法可能会尝试修改接收者。显然，它必须是在修改接收者的存储位置，而不是修改接收者值的副本然后将其丢弃。列表 9.11 中的示例 2 和示例 4 说明了这一事实如何影响在装箱值类型上调用方法调性能。

在示例 2 中，拆箱转换在逻辑上产生的是装箱后的值，而不是指向堆上包含装箱副本的存储位置的引用。那么，哪一个存储位置通过此传递给修改方法调用呢？它不可能是堆上箱的存储位置，因为拆箱转换产生的是该值的拷贝，而不是指向该存储位置的引用。

当这种情况发生时——需要值类型变量但只有一个值可用——会发生两种情况之一：C# 编译器生成代码，创建一个新的临时存储位置并将值从箱拷贝到新位置，从而导致该存储位置成为所需的变量；或者编译器产生错误并不允许分配。在这种情况下，使用了前一种策略。新的存储位置随后成为该调用的接收者；在它被修改后，装箱后的值被丢弃。

这个过程——对装箱后的值进行类型检查、拆箱以产生存储位置、分配临时变量、将值从箱拷贝到变量，然后使用临时存储的位置的位置调用方法——每当你使用“先拆箱后调用”的模式时都会发生，无论方法是否修改了该变量。显然，C# 编译器并不知道这些工作是否可以被避免。由于 C# 编译器不知道你调用的任何特定方法是否会尝试修改接收者，它必须采取谨慎的策略（err on the side of caution）。

在对装箱值类型上调用接口方法时，这些开销都被消除了。在这种情况下，预期接收者将是箱中的存储位置；如果接口方法修改了存储位置，那么应该修改的是箱中的位置。因此，避免了执行类型检查、分配新临时存储和进行拷贝的开销。相反，运行时直接使用箱中的存储位置作为调用结构体方法的接收者。

在列表 9.28 中，我们调用了位于 `IFormattable` 接口上的两个参数版本的 `ToString()` 方法，该接口由 `int` 类型实现。在这个示例中，调用的接收者是一个装箱后的值类型，但它没有为了调用接口方法而进行拆箱。

```
Listing 9.28: 避免拆箱和拷贝
int number;
object thing;
number = 42;
// 装箱
thing = number;
// 无拆箱转换
string text = ((IFormattable)thing).ToString("X", null);
Console.WriteLine(text);
```

现在假设我们将由 `object` 声明的虚拟 `ToString()` 方法替换为值类型的实例作为接收者。会发生什么呢？实例是被装箱的、拆箱的还是其他的？取决于细节，可能存在不同的场景：

- 如果接收者被拆箱且结构体重写了 `ToString()`，则直接调用重写的方法。不需要虚调用，因为该方法无法被更派生的类进一步重写；所有值类型都是自动密封的（sealed）。
- 如果接收者被拆箱且结构体没有重写 `ToString()`，则必须调用基类的实现，它期望一个对象引用作为接收者。因此，接收者被装箱。
- 如果接收者被装箱且结构体重写了 `ToString()`，箱中的存储位置将在不拆箱的情况下传递给重写的方法。
- 如果接收者被装箱且结构体没有重写 `ToString()`，指向箱的引用将传递给基类方法的实现，该实现期望的是一个引用。

# 枚举

比较列表 9.29 显示的两个代码片段。显然，可读性方面的差异是巨大的——在第二个片段中，分支情况（cases）是自文档的。然而，运行时的性能是相同的。为了实现这一结果，第二个片段使用了枚举值。

## 列表 9.29：比较整数 switch 和枚举 switch

```csharp
int connectionState;
// ...
switch (connectionState)
{
    case 0:
        // ...
        break;
    case 1:
        // ...
        break;
    case 2:
        // ...
        break;
    case 3:
        // ...
        break;
}
// ...
ConnectionState connectionState;
// ...
switch (connectionState)
{
    case ConnectionState.Connected:
        // ...
        break;
    case ConnectionState.Connecting:
        // ...
        break;
    case ConnectionState.Disconnected:
        // ...
        break;
    case ConnectionState.Disconnecting:
        // ...
        break;
}
```

枚举是开发者可以声明的一种值类型。枚举的关键特征是它在编译时声明了一组可以通过名称引用的可能值，从而使代码更易读。典型枚举声明的语法如列表 9.30 所示。

```
LISTING 9.30: 定义枚举
enum ConnectionState {
    Disconnected,
    Connecting,
    Connected,
    Disconnecting
}
```

> 注意
枚举也可以作为布尔值的更具读性的替代方案。例如，像 `SetState(true)` 这样的方法调用不如 `SetState(DeviceState.On)` 可读。

你通过通过枚举名称作为前缀来使用枚举值。例如，要使用 `Connected` 值，将使用 `ConnectionState.Connected` 语法。不要将枚举类型作为值名称的一部分，以避免 `ConnectionState.ConnectionStateConnected` 类似的引用的冗余。按照习惯，枚举名称本身应该是单数的（除非枚举值是位标志，稍后会讨论）。也就是说，命名法应该是 `ConnectionState` 而不是 `ConnectionStates`。

> 指南
不要将枚举类型作为值名称的一部分。
除非枚举是标志，否则使用单数枚举名称。

枚举值实际上实现为简单的整数常量。默认情况下，第一个枚举赋予值 0，随后的每个项目增加 1。或者，你可以为枚举成员分配明确的值，如列表 9.31 所示。

在此代码中，`Disconnected` 的默认值为 0，而 `Connecting` 被显式分配了 10；因此，`Connected` 将被分配 11。

被赋值为 11，这是赋值给 `Connected` 的值。（在这种情况下，不需要加枚举名称前缀，因为它出现在其作用域内。）`Disconnected` 的值为 12。

## 列表 9.31: 定义一个枚举类型

```sharp
enum ConnectionState : short
{
    Disconnected,
    Connecting = 10,
    Connected,
    Joined = Connected,
    Disconnecting
}
```

枚举始终有一个底层类型，该类型可以是除 `char` 以外的任何整数类型。事实上，枚举类型的性能与底层类型完全相同。默认情况下，底层的值类型是 `int`，但你可以使用继承语法指定不同的类型。例如，列表 9.15 使用了 `short` 而不是 `int`。为了保持一致性，枚举的语法模拟了继承的语法，但它并没有实际上创建继承关系。所有枚举的基类都是 `System.Enum`，它又派生自 `System.Value`。此外，这些枚举是密封的（sealed）；你不能从现有的枚举派生以更多成员。

## 指南

- 考虑使用默认的 32 位整数类型作为枚举的底层类型。只有在为了互操作性必须这样做时才使用较小的类型；只有当你创建一个带有超过 32 个标志的标志枚举（flags enum）¹时才使用较大的类型。

枚举本质上只是在底层类型上薄薄地覆盖了一层名称；没有任何机制可以将枚举变量的值限制为仅声明中命名的值。例如，由于可以将整数 42 强制转换为 `short`，因此也可以将整数 42 强制转换为 `ConnectionState` 类型，即使没有对应的 `ConnectionState` 枚举值。如果该值可以转换为底层类型，那么转换到枚举类型的转换也将是成功的。

10. 参见本章节后后部分“作为标志的枚举”节中的讨论。

这种奇特特征的优势是，可以在后续 API 发布中为枚举添加新值，而不会破坏早期的版本。此外，枚举值为已知值提供了名称，同时允许在运行时分配未知值。负担在于，开发者必须针对可能出现的未命名值进行防御性编码。例如，将 `ConnectionState.Disconnecting` 替换为 `default` 并期望 `default` 情况的唯一可能值是 `ConnectionState.Disconnect` 是不明智的。相反，你应该显式处理 `Disconnecting` 情况，并让 `default` 情况报告错误或表现无害。然而，如前面提到的，枚举与底层类型以及反向转换需要显式强制转换；它不是隐式转换。例如，如果方法的签名是 `void ReportState(ConnectionState state)`，则代码无法调用 `ReportState(10)`。这种异常仅发生在传递 0 时，因为 0 到任何枚举都有隐式转换。

虽然你可以在代码的后续版本中向枚举添加更多值，但你应该谨慎地这样做。在枚举中间插入枚举值将推后之后所有枚举值的值（例如，在 `Connected` 之前添加 `Flooded` 或 `Locked` 将改变 `Connected` 的值）。这将影响所有针对新版本重新编译的代码版本。然而，任何针对旧版本编译的代码将继续使用旧值，导致预期的值完全不同。除了在列表末尾插入枚举值外，避免更改枚举值的另一种种方法是显式地分配值。

## 第 9 章：介绍结构体和记录

## 指南

- 考虑向现有枚举添加新成员，但要记住兼容性风险。
- 避免创建代表“不完整”值集的枚举，例如产品版本号。
- 避免在枚举中创建“留供以后使用”的值。
- 避免创建包含单个值的枚举。
- 为简单枚举提供一个值为 0（none）的值，并知道在没有提供显式初始化时，0 将将是默认值。

## 高级主题

### 枚举之间的类型兼容性

C# 也不支持两个不同枚举数组之间的直接强制转换。然而，CLR（公共语言运行时）支持转换，只要这两个枚举共享相同的底层类型。为了绕过 C# 的这一限制，技巧是首先强制转换为 `System.Array`，如列表 9.32 结尾所示。

## 列表 9.32: 枚举数组之间的强制转换

```sharp
enum ConnectionState1
{
    Disconnected,
    Connecting,
    Connected,
    Disconnecting
}
enum ConnectionState2
{
    Disconnected,
    Connecting,
    Connected,
    Disconnecting
}
public class Program
{
    public static void Main()
    {
        ConnectionState1[] states = (ConnectionState1[])(Array)new ConnectionState2[42];
    }
}
```

此示例利用了 CLR 的赋值兼容性概念比 C# 的概念更宽松的特性。（其他非法转换也适用同样的技巧，例如从 `int[]` 到 `uint[]`）。然而，你应该谨慎地使用这种方法，因为没有 C# 规范要求这种行为在不同的 CLR 实现中生效。

## 枚举与字符串之间的转换

枚举相关的便利性之一是 `ToString()` 方法（由 `System.Console.WriteLine()` 等方法调用）会像列表 9.33 所示输出枚举值的标识符：

## 列表 9.33: 将枚举标识符写入缓冲区

```sharp
System.Diagnostics.Trace.WriteLine(
  "The connection is currently {ConnectionState.Disconnecting}");
```

之前的代码将输出 9.3 中的文本写入缓冲区。

## 输出 9.3

```
The connection is currently Disconnecting.
```

从字符串转换为枚举并不那么明显，因为它涉及到 `System.Enum` 基类。列表 9.34 提供了如何做的示例。

## 列表 9.34: 使用 Enum.TryParse 将字符串转换为枚举

```sharp
System.Diagnostics.Trace priority;
if(Enum.TryParse("Idle", out priority))
{
  System.Diagnostics.Trace.WriteLine(priority);
}
```

此示例描述了一种编译时的表示，字面量见第 18 章。`TryParse<T>` 方法使用了泛型，产生了列表 9 所示的等效语法。

## 枚举

无论代码使用 "Parse" 还是 "TryParse" 方法，关于字符串转换为枚举的关键警告在于强制转换是非优的，除非成功是肯定的。因此，开发者应该在消息未暴露给用户的情况下使用此类类型。

## 指南

- 避免枚举/字符串转换，除非字符串必须本地化。

很多时候，开发者不仅希望枚举值是唯一的，还希望能够表示组合。例如，考虑 `System.IO.FileAttributes`。这个枚举在列表 9.35 所示指示了文件的各种属性：只读、隐藏等。与 `ConnectionState` 属性（每个枚举值都是互斥）不同，`FileAttributes` 枚举值可以并且用于组合：一个文件可以是只读又是隐藏的。为了支持这种行为，每个枚举成员的值是一个唯一的位。

## 列表 9.35: 使用标志（Flags）枚举

```sharp
[Flags]
public enum {
    None = 0,                          // 000000000000
    ReadOnly = 1 << 0,                 // 000000000001
    Hidden = 1 << 1,                   // 000000000010
    System = 1 << 2,                  // 000000000100
    Directory = 1 << 4,               // 000000010000
    Archive = 1 << 5,                 // 000000100000
```
