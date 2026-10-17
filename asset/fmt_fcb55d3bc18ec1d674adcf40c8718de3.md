
清单 9.5 中显示的代码在编译后，在生成的 CIL 中会产生五个装箱指令和三个拆箱指令。

- 前两个装箱指令出现在对 `list.Add()` 的初始调用中。`ArrayList` 方法的签名为 `int Add(object value)`。因此，传递给此方法的任何值类型都会被装箱。
- 接下来是在 `for` 循环内调用 `Add()` 时的两个拆箱指令。`ArrayList` 索引运算符的返回类型始终是 `object`，因为 `ArrayList` 包含的就是 `object`。为了相加这两个值，你需要将它们转换回 `double`。这种从 `object` 引用到值类型的转换实现为拆箱调用。
- 现在你将加法的结果放入 `ArrayList` 实例中，这再次导致装箱操作。请注意，前两个拆箱指令和这个装箱指令都发生在循环内。
- 在 `foreach` 循环中，你遍历 `ArrayList` 中的每个项目并将其赋值给 `count`。如前所述，`ArrayList` 中的项目是对象引用，因此将它们赋值给 `double` 实际上是对每个项目进行拆箱。
- 在 `foreach` 循环中调用的 `Console.WriteLine()` 的签名是 `void Console.Write(string format, object arg)`。因此，每次调用都会将 `double` 装箱为 `object`。

每次装箱操作都涉及分配和复制；每次拆箱操作都涉及类型检查和复制。使用未装箱的类型执行等效的工作将消除分配和类型检查。显然，你可以通过消除许多装箱操作轻松提高此代码的性能。在最后一个 `foreach` 循环中使用 `object` 而不是 `double` 就是这种改进之一。另一种改进是将 `ArrayList` 的数据类型更改为泛型集合（参见第 12 章）。这里要说明的要点是，装箱可能相当微妙，因此开发人员需要特别注意并注意到它可能反复发生并影响性能的情况。

另一个不幸的装箱相关问题也发生在运行时：如果你想要修改初始的两个 `Add()` 调用，使其不使用转换（或 `double` 字面量），你就必须向数组列表插入整数。由于 `int` 会隐式转换为 `double`，这看起来是一个无害的修改。然而，`for` 循环内的 `double` 转换以及 `foreach` 循环中赋值给 `count` 时的转换将会失败。问题在于拆箱操作紧接着就是尝试将装箱的 `int` 值复制到 `double` 中。如果不先转换为 `int`，就无法完成此操作，因为代码在运行时将抛出 `InvalidCastException`。清单 9.6 展示了一个类似的错误（已注释掉）以及正确的转换方式。

### 清单 9.6：拆箱必须基于底层类型

```csharp

// ...

int number;

object thing;

double bigNumber;

number = 42;

thing = number;

// ERROR: InvalidCastException

// bigNumber = (double)thing;

bigNumber = (double)(int)thing;

// ...

```

### 进阶主题

### Lock 语句中的值类型

C# 支持 `lock` 语句来同步代码。该语句编译为 `System.Threading.Monitor` 的 `Enter()` 和 `Exit()` 方法。必须成对调用这两个方法。`Enter()` 会记录传入的唯一引用参数，以便当使用相同引用调用 `Exit()` 时，可以释放锁。使用值类型的问题在于装箱。因此，每次调用 `Enter()` 或 `Exit()` 时，都会在堆上创建一个新值。将一个副本的引用与另一个副本的引用进行比较始终返回 `false`，因此你无法将 `Enter()` 与对应的 `Exit()` 连接起来。因此，不允许在 `lock()` 语句中使用值类型。

清单 9.7 指出了更多运行时装箱的特异行为，输出 9.2 展示了结果。

### 清单 9.7：微妙的装箱特异行为

```csharp

interface IAngle

{

    void MoveTo(int degrees, int minutes, int seconds);

}

struct Angle : IAngle

{

    // ...

    // NOTE: This makes Angle mutable, against the general guideline

    public void MoveTo(int degrees, int minutes, int seconds)

    {

        _degrees = degrees;

        _Minutes = minutes;

        _Seconds = seconds;

    }

}

```

### 清单 9.7

```csharp

class Program

{

    static void Main()

    {

        // ...

        Angle angle = new Angle(25, 58, 23);

        // 示例 1：简单的装箱操作

        object objectAngle = angle;  // 装箱

        Console.Write( ((Angle)objectAngle).Degrees);

        // 示例 2：拆箱，修改拆箱后的值，并丢弃该值

        ((IAngle)objectAngle).MoveTo(26, 58, 23);

        Console.Write(", " + ((Angle)objectAngle).Degrees);

        // 示例 3：装箱，修改装箱后的值，并丢弃对装箱对象的引用

        ((IAngle)angle).MoveTo(26, 58, 23);

        Console.Write(", " + ((Angle)angle).Degrees);

        // 示例 4：直接修改装箱后的值

        ((IAngle)objectAngle).MoveTo(26, 58, 23);

        Console.WriteLine(", " + ((Angle)objectAngle).Degrees);

        // ...

    }

}

```

**输出 9.2**

```
25, 25, 25, 26
```

清单 9.7 使用了 `Angle` 结构体和 `IAngle` 接口。此外请注意，`IAngle.MoveTo()` 接口使 `Angle` 变得可修改。这一变化揭示了可变值类型的一些特异性，并借此展示了遵循“使结构体不可变”这一准则的重要性。

在清单 9.7 的示例 1 中，初始化 `angle` 后，将其装箱到一个名为 `objectAngle` 的变量中。接下来，示例 2 调用 `MoveTo()` 试图将 `Hours` 修改为 26。然而，正如输出结果所示，第一次操作实际上并未发生更改。问题在于，为了调用 `MoveTo()`，编译器会对 `objectAngle` 进行拆箱，并（根据定义）创建该值的一个副本。值类型是按值复制的——这正是它们被称为值类型的原因。尽管在运行时该副本的值被成功修改了，但这个值的副本随后被丢弃，因此 `objectAngle` 引用的堆内存位置没有发生任何变化。

回想一下我们的类比：建议将值类型变量想象成写有值的纸片。当你装箱一个值时，你复印了这张纸片并将副本放入盒子中。当你拆箱该值时，你复印了盒子中的纸片。修改第二张副本（拆箱得到的副本）并不会改变盒子中保留的那张副本。

在示例 3 中，类似的问题以相反的方式发生。没有直接调用 `MoveTo()`，而是将该值强制转换为 `IAngle`。转换为接口类型会对该值进行装箱，因此运行时会将 `angle` 中的数据复制到堆上，并提供对该盒子的引用。接着，方法调用修改了引用盒子中的值。存储在变量 `angle` 中的值保持不变。

在最后一个示例中，转换为 `IAngle` 是引用转换，而不是装箱转换。在这种情况下，该值已经通过转换为 `object` 被装箱了，因此在此转换过程中不会发生值的复制。对 `MoveTo()` 的调用更新了存储在盒子中的 `Hours` 值，代码的表现符合预期。

从这个示例中可以看出，可变值类型非常令人困惑，因为通常很难判断你是在修改值的副本，还是实际想要更改的存储位置。通过从一开始就避免使用可变值类型，你可以消除这类困惑。

## 准则
- 避免使用可变值类型。

## 高级主题

### 如何在方法调用中避免装箱

每当在值类型上调用方法时，接收调用（在方法体中由 `this` 表示）的值类型必须是一个变量，而不是一个值，因为该方法可能试图修改接收者。显然，它必须修改接收者的存储位置，而不是修改接收者值的副本然后丢弃它。清单 9.7 中的示例 2 和示例 4 说明了这一事实如何影响对装箱值类型进行方法调用的性能。

在示例 2 中，拆箱转换在逻辑上产生的是装箱值，而不是指向堆内存中包含装箱副本的存储位置的引用。那么，哪个存储位置被作为 `this` 传递给修改型方法调用？它不可能是堆内存中盒子的存储位置，因为拆箱转换产生的是该值的副本，而不是指向该存储位置的引用。

当出现这种情况——需要一个值类型变量但只有值可用时——会发生以下两种情况之一：要么 C# 编译器生成代码创建一个新的临时存储位置，并将值从盒子中复制到新位置，使得该临时存储位置成为所需的变量；要么编译器产生错误并禁止该操作。在这种情况下，采用了前一种策略。新的临时存储位置成为调用的接收者；在它被修改后，临时存储位置被丢弃。

这个过程——执行装箱值的类型检查、拆箱以产生装箱值的存储位置、分配临时变量、将值从盒子复制到临时变量、然后使用临时存储位置的地址调用方法——每次使用“拆箱然后调用”模式时都会发生，无论该方法是否实际修改变量。显然，如果该方法不修改变量，则可以避免其中的一些工作。由于 C# 编译器不知道你所调用的特定方法是否会试图修改接收者，它必须谨慎行事。

在对装箱值类型调用接口方法时，上述所有开销都被消除了。在这种情况下，预期接收者是盒子中的存储位置；如果接口方法修改存储位置，则应该是修改那个装箱的位置。因此，避免了执行类型检查、分配新的临时存储以及创建副本的开销。相反，运行时直接使用该盒子中的存储位置作为调用结构体方法的接收者。

在清单 9.8 中，我们调用了 `IFormattable` 接口上的双参数版本 `ToString()`，该接口由 `int` 值类型实现。在此示例中，调用的接收者是装箱值类型，但没有进行拆箱以调用接口方法。

### 清单 9.8：避免拆箱和复制

```csharp

int number;

object thing;

number = 42;

// 装箱

thing = number;

// 没有拆箱转换

string text = ((IFormattable)thing).ToString(

      "X", null);

Console.WriteLine(text);

```

此时你可能会想：假设我们改用值类型的实例作为接收者，调用了由 `object` 声明的虚方法 `ToString()`，会发生什么？实例是被装箱、拆箱，还是其他情况？根据具体情况，可能会发生几种不同的场景：

- 如果接收者是已拆箱的，并且结构体重写了 `ToString()`，则直接调用重写的方法。由于该方法无法被更派生的类进一步重写（所有值类型自动密封），因此不需要虚调用。
- 如果接收者是已拆箱的，并且结构体未重写 `ToString()`，则必须调用基类的实现，而基类实现期望接收一个 `object` 的引用作为接收者。因此，接收者会被装箱。
- 如果接收者是已装箱的，并且结构体重写了 `ToString()`，则盒子中的存储位置会直接传递给重写方法，而不会进行拆箱。
- 如果接收者是已装箱的，并且结构体未重写 `ToString()`，则盒子的引用会传递给该方法基类的实现，而基类实现期望的是一个引用。

## 枚举类型

比较清单 9.9 中显示的两个代码片段。

### 清单 9.9：比较整数 Switch 语句和枚举类型 Switch 语句

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

显然，在可读性方面的差异是巨大的——在第二个片段中，各情况分支具有自文档化特性。然而，运行时的性能是相同的。为了达到这一结果，第二个片段在每个分支中使用了**枚举值**。

枚举类型是一种开发人员可以声明的值类型。枚举类型的关键特性在于它在编译时声明了一组可以通过名称引用的可能常量值，从而使代码更易读。典型枚举类型声明的语法如清单 9.10 所示。

### 清单 9.10：定义枚举类型

```csharp

enum ConnectionState

{

    Disconnected,

    Connecting,

    Connected,

    Disconnecting

}

```

> **注意**
枚举也可以用作布尔值的更具可读性的替代方案。例如，像 `SetState(true)` 这样的方法调用，其可读性不如 `SetState(DeviceState.On)`。

使用枚举值时，需要在其前面加上枚举名称。例如，若要使用 `Connected` 值，你应使用语法 `ConnectionState.Connected`。请勿将枚举类型名作为值名的一部分，以避免出现诸如 `ConnectionState.ConnectionStateConnected` 这样的冗余。按照惯例，枚举名称本身应为单数（除非枚举是位标志，这一点将在后面讨论）。也就是说，命名规范应为 `ConnectionState`，而不是 `ConnectionStates`。

枚举值实际上只是整数常量。默认情况下，第一个枚举值被赋予 0，随后的每一项递增 1。但是，你可以为枚举分配显式值，如清单 9.11 所示。

## 清单 9.11：定义枚举类型

```
enum ConnectionState : short
{
    Disconnected,
    Connecting = 10,
    Connected,
    Joined = Connected,
    Disconnecting
}
```
