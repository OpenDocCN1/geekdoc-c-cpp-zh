
在 C# 中，可以通过以下三种方式之一来声明和使用类：

- 在程序所在的源代码文件中声明，例如 `Form1.cs`。
- 向项目中添加一个单独的 `.cs` 文件，然后在该文件中声明并编写新类。
- 在 Visual Studio 中创建一个完全独立的库文件来声明类，该库文件会保存为 `.dll` 文件，可供分发并在任何 C# 项目中使用。

类结构的通用模板如下：

```csharp
class name_of_the_class
{
    variable_type variable_1;
    variable_type variable_2;
    .
    .
    variable_type variable_n;

    return_type method_1(params_1)
    {
        method_1 code here
    }
    return_type method_2(params_2)
    {
        method_2 code here
    }
    .
    .
    .
    return_type method_m(params_m)
    {
        method_m code here
    }
}
```

代码 12.1

在该模板中，类内部包含多个变量（成员变量）和方法。

### 12.2. 在同一文件中声明类

在本示例中，我们将在主程序中声明一个类，该类中包含一个执行加法运算的方法。

- 1. 创建一个新的 C# 项目。
- 2. 在窗体上添加三个 TextBox 和一个 Button。
- 3. 将 TextBox 的 Name 分别设置为 `input1`、`input2` 和 `output`。
- 4. 将 Button 的 Name 和 Text 属性分别设置为 `addButton` 和 `Add`。此时窗体如下图所示：

![](img/41d82527c4e41cdb7e56259564306ddc_298_0.png)

图 12.2 窗体布局

- 5. 右键单击窗体上的空白处，选择“查看代码”，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_298_1.png)

图 12.3 打开 Form1.cs 的代码视图

- 6. 我们将在 `Form1.cs` 文件中添加名为 `AddClass` 的新类。如图 12.4 所示，`Form1.cs` 中已经有一个名为 `Form1` 的类。因此，我们的新类将放在该类声明结束位置的下方，如图 12.5 所示。

```csharp
private void addButton_Click(object sender, EventArgs e)
{
    int input1Num = Convert.ToInt32(input1.Text);
    int input2Num = Convert.ToInt32(input2.Text);
}
```

代码 12.4

- 10. 为了使用该类的变量和方法，我们需要声明一个该类的对象。我们需要为这个对象命名，比如 `myObject`：

```csharp
private void addButton_Click(object sender, EventArgs e)
{
    int input1Num = Convert.ToInt32(input1.Text);
    int input2Num = Convert.ToInt32(input2.Text);
    AddClass myObject = new AddClass();
}
```

代码 12.5

请注意最后一行代码中如何使用 `new` 关键字声明对象。

- 11. 对象 `myObject` 现在拥有 `AddClass` 类所有的变量和方法的副本。我们将使用点号表示法把 `input1Num` 和 `input2Num` 变量传递给对象的 `num1` 和 `num2` 变量：

```csharp
private void addButton_Click(object sender, EventArgs e)
{
    int input1Num = Convert.ToInt32(input1.Text);
    int input2Num = Convert.ToInt32(input2.Text);
    AddClass myObject = new AddClass();
    myObject.num1 = input1Num;
    myObject.num2 = input2Num;
}
```

代码 12.6

通过这些代码行，我们将 `myObject` 的 `num1` 和 `num2` 变量分别设置为 `input1Num` 和 `input2Num`。

- 12. 最后，我们将调用 `myObject` 的 `AddMethod()` 方法，该方法将返回 `myObject` 中 `num1` 和 `num2` 的和：

```csharp
private void addButton_Click(object sender, EventArgs e)
}
}
```

代码 12.8

- 13. 生成并运行项目。程序窗口将如下图所示：

![](img/41d82527c4e41cdb7e56259564306ddc_303_0.png)

图 12.6 程序窗口

当我们输入两个数字并单击 Add 按钮时，程序会使用 `myObject`（派生自 `AddClass` 类）的 `AddMethod()` 方法进行加法运算，然后计算结果将显示在输出 TextBox 中：

![](img/41d82527c4e41cdb7e56259564306ddc_303_1.png)

图 12.7 使用我们声明的方法正确执行了加法运算

### 12.3. 在新文件中声明类

当我们有多个类时，最好将它们放在单独的文件中，并在需要时添加到项目中。在单独的文件中定义类很容易，但有一条重要规则：类名和文件名必须相同。让我们开发一个小项目，在一个新文件中创建一个类。

- 1. 创建一个新的 C# 项目。
- 2. 在窗体上添加两个 Button 和一个 Label。
- 3. 将 Button 的 Name 分别设置为 **firstMessageButton** 和 **secondMessageButton**，Text 分别设置为 **First message** 和 **Second message**。
- 4. 将 Label 的 Name 和 Text 分别设置为 **messageLabel** 和 **Message will appear here**。窗体可能如下图所示：

![](img/41d82527c4e41cdb7e56259564306ddc_304_0.png)

图 12.8 窗体布局

- 5. 当第一个 Button 被单击时，第一条消息将显示在 Label 上。同样，第二个 Button 会在 Label 上显示另一条消息。我们将使用一个类的某个方法来实现这些功能，该类定义在一个单独的文件中。要向项目添加类，请单击“项目”→“添加类...”，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_304_1.png)

图 12.9 向项目添加新类

- 6. Visual Studio 将要求输入类文件的名称。我将其命名为 `MessageClass.cs`：

![](img/41d82527c4e41cdb7e56259564306ddc_305_0.png)

图 12.10 命名类文件

单击“添加”后，新文件将被创建并在编辑器中打开：

![](img/41d82527c4e41cdb7e56259564306ddc_305_1.png)

图 12.11 在编辑器中打开的类文件

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Classes2
{
    class MessageClass
    {
        public string FirstMessage()
        {
            return "This is the first message coming from the " +
                   "FirstMessage method of the MessageClass.";
        }
        public string SecondMessage()
        {
            return "This is the second message coming from the " +
                   "SecondMessage method of the MessageClass.";
        }
    }
}
```

代码 12.14 – MessageClass.cs 文件

- 10. 生成并运行项目。Label 的 Text 将根据单击的 Button 而改变。将调用 `FirstMessage()` 或 `SecondMessage()` 方法，并在 Label 上显示第一条或第二条消息：

![](img/41d82527c4e41cdb7e56259564306ddc_309_0.png)

图 12.13 使用 `FirstMessage()` 方法返回的字符串在 Label 上显示第一条消息

![](img/41d82527c4e41cdb7e56259564306ddc_310_0.png)

图 12.14 使用 `SecondMessage()` 方法返回的字符串在 Label 上显示第二条消息

### 12.4. 构造方法

构造方法是在创建类的实例（即对象）时执行的特殊方法。即使我们不显式声明，所有类在后台都有各自的默认构造函数。类的构造方法在创建对象时只会执行一次。构造方法的主要职责是为成员变量分配内存并初始化这些变量。

构造方法的名称必须与类名相同。回想一下，我们在前面的示例（代码 12.13）中是如何从 `MessageClass` 创建 `firstObject` 对象的：

```csharp
MessageClass firstObject = new MessageClass();
```

代码 12.15

在这行代码中，我们创建了 `MessageClass` 的一个实例：名为 `firstObject` 的对象。为此，我们使用了 `new` 关键字，后跟构造方法 `MessageClass()`。

尽管所有类都像本示例中那样自动拥有默认的不可见构造方法，但我们也可以显式声明构造方法，主要用于向成员变量传递参数。

