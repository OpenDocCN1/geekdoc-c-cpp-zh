

## 第7章 组装一个 C# 程序

到目前为止，我们只看到过 C# 的一些片段，一段文件中的几行代码。更有趣的程序通常由许多文件组成，所以在本章中让我们提升一下水平，专注于从多个文件构建一个程序。而且，如果你还记得，“Hello, World!” 中有几行我们还没有解释，因为这些行在你学会如何用多于一个文件编写程序后更容易理解。在本章中我们也会讲解这些行，所以我们将最后再看一次 “Hello, World!” 。我们刚刚添加到项目中的文件包含一个与文件名相同的类。把一个文件对应一个类，并且文件名与类名相同，这是一种常见做法。

```
namespace MyUtilities
{
    class WeatherUtilities
    {
        static float FahrenheitToCelsius(float temperatureFahrenheit)
        {
            var temperatureCelsius = temperatureFahrenheit - 32 / 1.8f;
            return temperatureCelsius;
        }

        static float CelsiusToFahrenheit(float temperatureCelsius)
        {
            var temperatureFahrenheit = temperatureCelsius * 1.8f + 32;
            return temperatureFahrenheit;
        }

        static float ComfortIndex(float temperatureFahrenheit, float humidityPercent)
        {
            var comfortIndex = (temperatureFahrenheit + humidityPercent) / 4;
            return comfortIndex;
        }
    }
}
```

这当然不是强制性的，但这是一种方便的默认方式来在文件中组织类。而这个类包含几个静态方法，一个、两个、四个方法。它就像一个做天气计算的小型库。

```
static float FahrenheitToCelsius(float temperatureFahrenheit)
{
    var temperatureCelsius = temperatureFahrenheit - 32 / 1.8f;
    return temperatureCelsius;
}

static float CelsiusToFahrenheit(float temperatureCelsius)
{
    var temperatureFahrenheit = temperatureCelsius * 1.8f + 32;
    return temperatureFahrenheit;
}

static float ComfortIndex(float temperatureFahrenheit, float humidityPercent)
{
    var comfortIndex = (temperatureFahrenheit + humidityPercent) / 4;
    return comfortIndex;
}

static void Report(string location, float temperatureCelsius, float humidity)
{
    var temperatureFahrenheit = CelsiusToFahrenheit(temperatureCelsius);
    Console.WriteLine("Comfort Index for " + location + ": " + ComfortIndex(temperatureFahrenheit
```

这些方法建立在我们之前的示例之上。所以我们有从华氏度到摄氏度的转换，你可能还记得这个，还有反过来，从摄氏度到华氏度。我还添加了这个计算称为 ComfortIndex 的方法。它接受温度和湿度百分比作为输入，所以是一个 0 到 100 的数字。它返回一个任意的指数，本质上告诉你在这种温度和湿度下进行身体锻炼是否舒适。舒适这个概念很模糊。有很多可能的计算舒适度或体感温度以及类似指数的方法。我在网上找到的这个公式只是温度加湿度除以 4，指数越低，进行身体锻炼就越舒适。这当然不是一个非常可靠的指数，但它很简单，对于平均温度和湿度来说也算凑合，所以暂时就用它了。最后，我们有这个 Report() 方法。它接受一个字符串，应该是地点的名称，以及它的温度和湿度，并在屏幕上打印一份简短的报告，显示该地点的舒适指数。+ 运算符作用于字符串意味着连接这些字符串。所以这是字符串 Comfort Index for，后跟地点的名称，然后是冒号，然后是这个其他方法计算的 ComfortIndex。注意 ComfortIndex 不是一个字符串；它是一个 float。但当我们把它连接到一个字符串时，C# 会自动把它从 float 转换为字符串。我们知道 C# 对类型很挑剔，所以它不会让我们隐式转换类型，除非是安全的转换，而这就是一种安全的转换。你总能把浮点数转换为字符串而不会出错，所以把一个 float 连接到一个字符串是可以的，就像这里一样。所以，这就是我设计的类。我称它为库类。但说到这个，我们需要关于库这个概念做一个小 digression。我告诉你我写了这个包含实用方法的类，它就像一个小库。我把这个类添加到项目中，以便从我们的程序中使用它。只是为了说清楚，我不想给你错误的暗示，鼓励你这样编码。在大多数情况下，当你想要共享像库这样的功能时，你导入编译好的库，而不是库的源代码。如果你习惯于编译型语言，你会想，当然了。但如果你更习惯于解释型语言，那么花一点时间在这个区别上是值得的。你还记得我早些时候告诉过你，一个 C# 项目会生成一个 assembly，一个文件或有时是一小堆文件吗？所以，假设我们有一个项目交付一个 Windows 可执行文件，并且这个项目依赖于一个库，一个 DLL。一般来说，你不需要库的源代码；你只需要拿编译好的库，一个 DLL 文件，把它放到项目中，并告诉 Visual Studio 该项目依赖于这个 DLL。然后当你编译项目时，Visual Studio 会把可执行文件和 DLL 放在同一个目录下，这样可执行文件在运行时可以看到 DLL，一切都能正常工作。并且在 Visual Studio 中让 DLL 对项目可见还有其他方法。你可以把 DLL 放在机器上的一个全局区域，使其对任何项目可见，或者使用 NuGet 包管理器从互联网安装库，所有这些都超出了本书的范围。但有一点对所有这些情况都是共同的：你不需要源代码。你通常共享编译好的代码，而不是源代码。我在我们这种情况下使用源代码的原因是，我们想要修改这段代码，而这正是我们接下来要做的。在我们继续在程序中使用它之前，我们可以在这个类中改进几件小事，虽然小，但它们会累积起来。首先，我们可以添加注释。我确实尝试让这段代码使用显式的变量名，比如这里等等，但有时你确实需要注释。例如，我们说过计算舒适指数的这个公式可能不是最准确的方法，所以让我们写一个关于它的注释。如果你输入双斜杠，后面所有内容都是注释，直到行尾。说实话，这就是我最终会后悔的那种注释，因为过一段时间我再回来看我的代码，我本应该修复这段代码，而不是评论它不怎么样。但在这种情况下，我计划在完成本书写作后就不再更新这段代码，所以也许这次我能蒙混过关。另一个值得注释的事情是，当我们调用 ComfortIndex() 时，我们需要记住指数越高舒适度越低。这并不直观。很容易弄错。所以让我们写一个关于它的注释。我们见过用双斜杠的注释，但 C# 中还有其他类型的注释。

```
```csharp
// This is a comment until the end of the line

/*
 * This is a comment that
 * spans multiple lines.
 */

/// <summary>This is a <i>formatted</i> comment.</summary>
```
```

你可以写一个跨越多行的注释，以斜杠星序列开头，以星斜杠序列结尾。许多人也会再加几个星号让它看起来更漂亮。你也可以写带高级格式的注释，用于生成类和方法等的文档。但双斜杠可能是注释代码最常见的方式。除了注释之外，我们还可以对这个类做另一个小的改进，这个方法定义了一个变量然后返回它，但我们不需要这个中间变量。我们可以直接计算并立即返回结果。这是一种小重构，正如他们所说的，不改变代码行为的内部更改，因为这个方法返回的结果与之前相同。但大多数程序员会觉得它更易读。这两个方法也创建了我们可以删除的临时变量，但这次，与其手工做，让我们请 Visual Studio 来帮我们做。

