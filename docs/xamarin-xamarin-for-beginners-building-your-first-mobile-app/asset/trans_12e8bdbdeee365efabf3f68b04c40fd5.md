
我们正在编写的程序将显示在不同尺寸的屏幕上，因此我们希望让 GetNamedSize 函数进行正确的计算，以根据程序当前所处的屏幕尺寸以及要获取的尺寸返回合适的字号（在我们的示例中，我们想要得到一个大字号 NamedSize.Large，其他尺寸当然也存在）。

程序的其余部分非常简单，在第44行，我们将 formattedString 变量赋给了标签的 FormattedText 属性。这可以确保文本以格式化形式显示在屏幕上；请注意，在这种情况下我们没有使用 Text 属性。

最后一点需要注意。请注意，在第46行，我们为标签的 FontSize 属性分配了一个新的字号。这个字体将是中等大小（注意第一个参数 NamedSize.Medium）。这里的思路是：如果某段文本（包含在 Span 对象中）的 FontSize 属性未设置，那么这个字体将应用于该段文本。例如，这个字号不会应用于第34至39行指定的文本部分；正如我们之前看到的，该部分已经设置了自己的字号（NamedSize.Large）。

注意：要尝试此程序，你需要修改 App.cs 文件中的 App 构造函数。确保构造函数如下所示，以使用我们的新类 FormattedParagraphPage：

```csharp
public App()
{
    // The root page of your application
    MainPage = new FormattedParagraphPage();
}
```

## 结论

在本课中，我们介绍了 Xamarin 中文本处理的原理，并首次构建了两个向用户显示信息的简单应用。我们学习了如何对齐文本，以及执行一些格式化操作，例如更改任意单词或短语的文本颜色和背景颜色。本课没有涉及如何处理文本较大、需要一种方式来滚动显示其全部内容的情况。我们将在后续课程中解决这个问题。

## 第三章
### Xamarin 中的 StackLayout

在前面的课程中，我们只处理了屏幕上出现的一个元素。这个元素是 Label，我们把它赋给了内容页的 Content 属性。众所周知，在真实程序中，我们肯定需要许多元素出现在屏幕上，以满足程序的需求。这里的问题是，内容页的 Content 属性只接受一个继承自 View 类的元素。

Xamarin 使用布局为这个问题找到了一个简单的解决方案。布局可以容纳任意数量的项，这些项都继承自 View 类。实际上，布局本身继承自 `Layout<View>` 类，而 `Layout<View>` 类间接继承自 View 类。任何布局都可以直接赋给 Content 属性。Xamarin 支持四种类型的布局：

- AbsoluteLayout
- Grid
- RelativeLayout
- StackLayout

在本系列中，我们将介绍三种布局：AbsoluteLayout、RelativeLayout 和 StackLayout。本章我们先从 StackLayout 开始。

### StackLayout 堆叠布局

此布局中可以添加任意数量的项。之所以叫这个名字，是因为它排列的是堆叠起来的元素。与其他布局相比，StackLayout 类多了两个属性：Orientation 表示方向（水平或垂直），Spacing 表示添加到布局中的元素之间的间距，默认值为 6.0。现在让我们看一个简单的例子，来了解如何使用这个实用的布局。

### ColorsApp 应用：显示一些颜色

按照我们在前几课中学习的方法创建一个新应用，类型为空白应用（Xamarin.Forms Portable），并将其命名为 ColorsApp。在 Visual Studio 中创建应用后，只保留 ColorsApp（Portable）和 ColorsApp.Droid 项目。

将名为 ColorsListPage 的内容页添加到 ColorsApp（Portable）项目中（右键单击项目，选择“添加”，然后选择“新建项”。窗口出现后，从左侧选择“跨平台”，然后在屏幕中央选择“Forms ContentPage”）。创建此页面后，我们会注意到它已经自带了一个堆叠布局。看一下这个页面的内容：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Reflection.Emit;
using System.Text;

using Xamarin.Forms;

namespace ColorsApp
{
    public class ColorsListPage : ContentPage
    {
        public ColorsListPage()
        {
            Content = new StackLayout
            {
                Children = {
                    new Label { Text = "Hello ContentPage" }
                },
            };
        }
    }
}
```

请注意，在 ColorsListPage 构造函数中，我们将 StackLayout 类的一个新对象赋给了 Content 属性。还要注意，StackLayout 布局有一个名为 Children 的属性，它表示我们想要添加到堆叠中的子元素（每个子元素都继承自 View 类）。

将 ColorsListPage.cs 文件的内容替换为以下代码：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Reflection.Emit;
using System.Text;

using Xamarin.Forms;

namespace ColorsApp
{
    public class ColorInfo
    {
        public Color Color { get; set; }
        public string Name { get; set; }
    }

    public class ColorsListPage : ContentPage
    {
        public ColorsListPage()
        {
            ColorInfo[] colors = new ColorInfo[]
            {
                new ColorInfo { Color = Color.Aqua, Name = "Aqua" },
                new ColorInfo { Color = Color.Blue, Name = "Blue" },
                new ColorInfo { Color = Color.Gray, Name = "Gray" },
                new ColorInfo { Color = Color.Black, Name = "Black" },
                new ColorInfo { Color = Color.Silver, Name = "Silver" },
                new ColorInfo { Color = Color.Red, Name = "Red" },
                new ColorInfo { Color = Color.Maroon, Name = "Maroon" },
                new ColorInfo { Color = Color.Yellow, Name = "Yellow" },
                new ColorInfo { Color = Color.Olive, Name = "Olive" },
                new ColorInfo { Color = Color.Lime, Name = "Lime" },
                new ColorInfo { Color = Color.Green, Name = "Green" },
                new ColorInfo { Color = Color.Navy, Name = "Navy" },
                new ColorInfo { Color = Color.Teal, Name = "Teal" },
                new ColorInfo { Color = Color.Pink, Name = "Pink" },
                new ColorInfo { Color = Color.Fuchsia, Name = "Fuchsia" },
                new ColorInfo { Color = Color.Purple, Name = "Purple" }
            };

            StackLayout stackLayout = new StackLayout();

            for (int i = 0; i < colors.Length; i++)
            {
                stackLayout.Children.Add(new Label
                {
                    Text = colors[i].Name,
                    TextColor = colors[i].Color,
                    FontSize = Device.GetNamedSize(NamedSize.Large, typeof(Label))
                });
            }

            Padding = new Thickness(5, 5, 5, 5);

            Content = stackLayout;
        }
    }
}
```

我们在该文件中添加了一个名为 ColorInfo 的新简单类（第11至15行）。虽然同一个文件中有两个类通常不是好的软件实践，但我选择了简化处理。这个类的作用是保存任何颜色值及其名称的简单信息。在第21行，我们创建了一个 ColorInfo 类数组，并将其赋给 colors 变量。这个数组显然包含16种颜色。然后，我们创建 StackLayout 类的一个新对象，并将其赋给 stackLayout 变量（第41行），接着进入一个 for 循环（第43行），遍历 colors 数组中的元素，并通过 Children 属性将它们添加到 StackLayout 中。接下来，确定页面的内边距值（第53行），最后将 stackLayout 变量赋给页面的 Content 属性（第55行）。

要尝试此应用，请先转到 App.cs 文件，并确保 App 类的构造函数如下所示：

```csharp
public App()
{
    // The root page of your application
    MainPage = new ColorsListPage();
}
```

### 使用 F5 运行程序，外观与下面类似：

这里有两件重要的事情。首先，有些颜色在黑色背景（Android 上 Xamarin 应用的默认背景）上显示效果不佳，因为颜色对比度不够好；而 Black（黑色）这个词不会显示出来，因为它的颜色与黑色背景颜色相近。其次，我们基本上有16种颜色，但只出现了其中的12种。你看到的颜色数量可能会因所用屏幕的不同而有所差异。例如，它们可能全部出现，但无论如何，你一定会遇到
