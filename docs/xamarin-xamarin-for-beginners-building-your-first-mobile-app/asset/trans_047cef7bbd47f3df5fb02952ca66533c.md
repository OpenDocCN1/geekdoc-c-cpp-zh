

请注意，LayoutOptions.Center 被分别赋给 HorizontalOptions 和 VerticalOptions，以实现水平和垂直居中。再次运行程序，你会注意到，标签位于屏幕中央，如下图所示：

![](img/affff2e3b09de80cc0ffe811bbf63f5d_20_0.png)

如果你希望标签中的文本使用不同的颜色，比如红色，在这种情况下，请将 Color.Red 值赋给标签对象的 TextColor 属性。Color 也是 Xamarin.Forms 命名空间中的一个结构。

## 处理文本片段

我们经常需要在屏幕上显示一段文本。这段文本可能来自文档、Web 服务或其他来源。应用程序应该能够处理这种大小的文本。与上一课一样，我们创建了一个名为 TextManipulationApp 的新 Blank App（Xamarin.Forms Portable）项目。只保留 TextManipulationApp（Portable）和 TextManipulationApp.Droid 项目。

现在我们添加一个新的内容页，但采用与上一课不同且更简洁的方式。右键单击项目（TextManipulationApp（Portable）），选择“添加”，然后在出现的子菜单中选择“新建项”。在出现的窗口左侧选择“跨平台”节点，更新窗口中间部分的内容后，选择文件类型，在底部的“名称”框中，单击“添加”。

![](img/affff2e3b09de80cc0ffe811bbf63f5d_22_0.png)

在 Visual Studio 添加此文件后，其内容将如下所示：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Reflection.Emit;
using System.Text;

using Xamarin.Forms;
namespace TextManipulationApp
{
public class ParagraphPage: ContentPage
{
public ParagraphPage ()
{
Content = new StackLayout
{
Children = {
new Label {Text = "Hello ContentPage"}
}
};
}
}
}
```

这里有一些不必要的命名空间，但目前没什么问题。请注意，ParagraphPage 类默认继承自 ContentPage 类，并且 ParagraphPage 类构造函数已就绪，其中包含一个简单的示例。删除该构造函数的内容，让我们开始处理我们的应用程序。我们将创建一个 Label，其中包含一段阿拉伯语文本片段。将以下代码输入到 ParagraphPage 类构造函数中：

```
Content = new Label
{
```

```
VerticalOptions = LayoutOptions.Center,
    Text = "Xamarin is currently one of the most important mobile app development platforms available," +
    "Which seems to stay on the front for not too long," +
    "Especially after Microsoft acquired the company that also has the same name." +
    "Through this series we will learn to write practical applications by using this promising technology."
};
```

转到 TextManipulationApp（Portable）项目中的 App.cs 文件，确保应用类构造函数如下所示：

```
public App ()
{
// The root page of your application
MainPage = new ParagraphPage ();
}
```

### 使用 F5 运行程序

请注意，所有文本在垂直方向上居中显示。这是因为将 LayoutOptions.Center 值分配给了 Label 的 VerticalOptions 属性。另请注意，上图中的文本向左对齐，而不是像阿拉伯语文本那样向右对齐。这是因为 Label 类的 HorizontalTextAlignment 属性（负责标签内文本的水平对齐）在运行程序时会具有默认值 TextAlignment.Start。TextAlignment 是一个枚举，包含三个值：Start、Center 和 End。由于移动设备的屏幕在水平方向上分为三个主要区域：Start 对应左侧区域，Center 对应中间（中央）区域，End 对应屏幕右侧区域，因此文本将向左对齐而不是向右对齐。如果我们想要将文本向右对齐，只需将 TextAlignment.End 值赋给 HorizontalTextAlignment 属性即可，我们稍后将这样做。从上图中还要注意的另一件事是，文本离屏幕边缘太近，几乎贴在了边缘上。解决这个问题很简单：为屏幕边缘添加内边距（Padding），这是一个可以通过编程方式分配给屏幕的小区域，通过它我们可以控制四边的边距空间。现在看看经过所需修改的 ParagraphPage 类构造函数：

```
public ParagraphPage ()
{
Content = new Label
{
VerticalOptions = LayoutOptions.Center,
Text = "Xamarin is currently one of the most important mobile app development platforms available," +
"Which seems to stay on the front for not too long," +
"Especially after Microsoft acquired the company that also has the same name." +
"Through this series we will learn to write practical applications through the use of this promising technology.",

HorizontalTextAlignment = TextAlignment.End
};

Padding = new Thickness (5, 5, 5, 5);
}
```

我们首先向 Label 添加了 HorizontalTextAlignment 属性，并为其分配了 TextAlignment.End 值，以使标签内的文本向右对齐（请注意，普通逗号分隔属性）。我们还添加了 Padding 属性（来自 ParagraphPage 类），并为其分配了一个新的 Thickness 类对象。Thickness 支持重载，因为它有多种形式。我使用了最后一种形式，它接受四个参数，分别代表左、上、右、下的内边距量。你可能对这里使用的一个类比感到疑惑，但我会把讨论推迟到

屏幕

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Reflection.Emit;
using System.Text;

using Xamarin.Forms;

namespace TextManipulationApp
{
public class FormattedParagraphPage: ContentPage
{
public FormattedParagraphPage ()
{
FormattedString formattedString = new FormattedString ();

formattedString.Spans.Add (new Span
{
Text = "Don't count",
});

formattedString.Spans.Add (new Span
{
Text = "Glory",
BackgroundColor = Color.Yellow,
ForegroundColor = Color.Blue,
});

formattedString.Spans.Add (new Span
{
Text = "Pass you eat",
});

```

```
formattedString.Spans.Add (new Span
{
    Text = "You will not attain glory until you lick patience.",
    ForegroundColor = Color.Aqua,
    FontSize = Device.GetNamedSize (NamedSize.Large, typeof
(Label))
});

Content = new Label
{
VerticalOptions = LayoutOptions.Center,
FormattedText = formattedString,
HorizontalTextAlignment = TextAlignment.End,
FontSize = Device.GetNamedSize (NamedSize.Medium, typeof (Label))
};

Padding = new Thickness (5, 5, 5, 5);
}
}
}
```

我们在构造函数（第 15 行）中首先创建了一个 FormattedString 类的对象，并将其分配给 formattedString 变量。然后我们开始使用以下简单方法（第 17 至 20 行）向 Spans 集合添加格式化文本：

```
formattedString.Spans.Add (new Span
{
Text = "Don't count"
});
```

我们使用 Spans 集合的 Add 函数来添加一个 Span 类型的对象，我们创建了该对象并在创建时直接为其分配了 Text 属性。前面代码中的文本没有任何特殊格式。实际上，我们对完整文本的每一部分都重复了这一方法。但有时我们采用了一些不同的文本格式。例如，请看第 22 至 27 行的代码：

```
formattedString.Spans.Add (new Span
{
Text = "Glory",
BackgroundColor = Color.Yellow,
ForegroundColor = Color.Blue,
});
```

这一次，我们设置了文本“Glory”的格式，为 BackgroundColor 指定了黄色作为背景色，为文本颜色 ForegroundColor 指定了蓝色。另请参见我们在第 34 至 39 行添加的文本部分：

```
formattedString.Spans.Add (new Span
{
Text = "You will not attain glory until you lick patience.",
ForegroundColor = Color.Aqua,
FontSize = Device.GetNamedSize (NamedSize.Large, typeof (Label))
});
```

这次字体颜色为 Aqua，字体大小为 Large。注意我们是如何将字体大小值赋给 FontSize 属性的。为此使用了以下表达式：

**Device.GetNamedSize (NamedSize.Large, typeof (Label))**

Device 表示我们的应用程序当前运行的设备，并包含许多有用的静态函数。在这些函数中，我们使用了 GetNamedSize 函数，它返回由传递给它的参数所要求的字体大小。第一个参数是 NamedSize.Large，所以我们想要一个大的字体大小（NamedSize 是一个枚举），第二个参数是应用该字体的元素类型。在这种情况下，我们希望将此字体应用到 Label，因此我们传递了 typeof (Label) 作为第二个参数，它会返回 Label 的类型。这是为你想到的任何内容设置合适尺寸的首选方法，因为设备我们

