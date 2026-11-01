

```
<td>
    <asp:Label Runat="server" ID="suitLabel">梅花</asp:Label>
</td>
</tr>
</table>
```

这为控件定义了一个默认状态：一张梅花图片和一个标签。图片路径中的 `~` 表示“从网站的根目录开始”。在添加功能之前，你将先把此控件添加到网页中，以测试这个默认状态。因此，在继续之前，请在网站中添加一个名为 Default.aspx 的新网页。

要在 .aspx 文件中使用自定义控件，首先需要指定如何引用它，也就是指定在 HTML 中代表该控件的标记名称。为此，需要在 Default.aspx 代码顶部使用 <%@ Register %> 指令，如下所示：

```
<%@ Register TagPrefix="pcs" TagName="UserCl" Src="PCSUserCl.ascx" %>
```

*代码片段 PCSUserCWebApp1/Default.aspx*

TagPrefix 和 TagName 属性用于指定要使用的标记名称（格式为 <TagPrefix:TagName>），而 Src 属性用于指向包含用户控件的文件。现在，你可以用以下代码替换文件中现有的 <form> 元素，从而使用该控件：

```
<form id="Form1" method="post" runat="server">
<div>
<pcs:UserCl Runat="server" ID="myUserControl"/>
</div>
</form>
```

这样就可以测试用户控件了。图 41-1 显示了运行此代码后的结果。

![](img/d7d2ffa0a76feaab821930e95daace93_1249_0.png)

图 41-1

目前，此控件在表格布局中组合了两个现有控件：一个图像和一个标签。因此，它属于复合控件。

## 添加 Suit 属性

若要控制显示的花色，可以在 <PCS:UserCl> 元素上使用属性。用户控件元素上的属性会自动映射到用户控件的属性，因此，要实现此功能，只需在控件的代码隐藏文件 PCSUserCl.ascx.cs 中添加一个属性即可。将此属性命名为 Suit，并使其接受任意花色值。为了更方便地表示控件状态，可以定义一个枚举来保存四种花色名称。最佳做法是在网站中添加一个 App_Code 目录，然后在此目录中添加一个名为 Suit.cs 的 .cs 文件。App_Code 是另一个“特殊”目录，和 App_Data 类似，其功能由系统定义；在这里，它用于存放网站的其他代码文件。你可以在解决方案资源管理器中右键单击网站，然后依次单击“添加 ASP.NET 文件夹”->“App_Code”，以添加此目录。完成后，添加 Suit.cs，并写入以下代码：

```csharp
using System;

public enum Suit
{
    Club, Diamond, Heart, Spade
}
```

代码片段 PCSUserCWebApp1/App_Code/Suit.cs

PCSUserCl 类需要一个成员变量 currentSuit，用于保存花色类型：

```csharp
public partial class PCSUserCl : System.Web.UI.UserControl
{
    protected Suit currentSuit;
}
```

代码片段 PCSUserCWebApp1/PCSUserCl.ascx.cs

还需要一个 Suit 属性来访问此成员变量：

```csharp
public Suit Suit
{
    get
    {
        return currentSuit;
    }
    set
    {
        currentSuit = value;
        suitPic.ImageUrl = "~/Images/" + currentSuit.ToString() + ".bmp";
        suitLabel.Text = currentSuit.ToString();
    }
}
```

此处的 set 访问器会将图像 URL 设置为你之前复制的其中一个文件，并将显示的文本设置为花色名称。

## 访问新属性

接下来，你必须向 Default.aspx 添加代码，以便访问这个新属性。你可以直接通过刚添加的属性指定花色（如果编译项目，IntelliSense 甚至会显示可用选项）：

```html
<PCS:UserCl Runat="server" id="myUserControl" Suit="diamond" />
```

代码片段 PCSUserCWebApp1/Default.aspx

ASP.NET 处理器能够根据提供的字符串自动获取正确的枚举项。不过，为了让示例更有趣、更具交互性，你将使用单选按钮列表来选择花色：

```html
<form id="form1" runat="server">
    <div>
        <pcs:UserCl id="myUserControl" runat="server" />
        <asp:RadioButtonList runat="server" ID="suitList" AutoPostBack="True">
            <asp:ListItem Value="Club" Selected="True">Club</asp:ListItem>
            <asp:ListItem Value="Diamond">Diamond</asp:ListItem>
            <asp:ListItem Value="Heart">Heart</asp:ListItem>
            <asp:ListItem Value="Spade">Spade</asp:ListItem>
        </asp:RadioButtonList>
    </div>
</form>
```

![](img/d7d2ffa0a76feaab821930e95daace93_1252_0.png)

图 41-3

除了通过主题实现的显而易见的样式变化（本章稍后会介绍）之外，主要改动如下：

- 用户名会自动从用户详细信息中获取。
- 页面底部不再显示额外数据，代码隐藏文件中相应的 DataBind() 调用也已移除。
- 控件下方不再显示结果标签——用户通过看到日历和事件列表中添加的事件，就能获得足够的反馈，无须再告知他们事件已成功添加。
- 包含用户控件的页面使用了导航控件和母版页。

实现这些改动所需的代码修改非常简单。这里不再介绍这些修改，但本章稍后会再次回到这个控件。

你也可以用非常相似的方式创建应被解释为其他控件子级的控件。这是更高级的技术之一，本书不会介绍。

## 自定义控件示例

现在是将部分理论付诸实践的时候了。你将在 C:\ProCSharp\Chapter41 目录中使用一个名为 PCS Custom Web Site1 的网站（通过空网站模板创建），并在其 App_Code 目录中添加一个自定义控件，以演示简单的自定义控件。这里的控件是现有 Label 控件的多彩版本，能够为文本中的每个字母轮流使用一组颜色。

文件 App_Code\RainbowLabel.cs 中 RainbowLabel 控件的代码以以下 using 语句开头：

```csharp
using System.Drawing;
using System.Web.UI;
using System.Web.UI.WebControls;
```

代码片段 PCS Custom Web Site1\RainbowLabel.cs

Color 枚举需要 System.Drawing 命名空间，而 ASP.NET 控件引用则需要 Web 命名空间。该类使用一个名为 colors 的私有 Color 数组，保存用于文本中字母的颜色：

```csharp
namespace PCSCustomWebControls
{
    public class RainbowLabel : Label
    {
        private Color[] colors = new Color[] {Color.Red,
            Color.Orange,
            Color.Yellow,
            Color.GreenYellow,
            Color.Blue,
            Color.Indigo,
            Color.Violet};
```

还要注意，控件被包含在命名空间 PCSCustomWebControls 中。正如前文所述，这是为了让网页能够正确引用该控件。

为了实现颜色循环，还需要在名为 offset 的私有属性中保存一个整数偏移值：

```csharp
private int offset
{
    get
    {
        object rawOffset = ViewState["_offset"];
        if (rawOffset != null)
        {
            return (int)rawOffset;
        }
        else
        {
            ViewState["_offset"] = 0;
            return 0;
        }
    }
    set
    {
        ViewState["_offset"] = value;
    }
}
```

请注意，这个属性并不像将值存储在成员字段中那么简单。这是由 ASP.NET 维护状态的方式决定的，具体内容可参见上一章。每次回发操作都会实例化控件，因此要保存值，必须使用视图状态。访问视图状态很简单——只需使用 ViewState 集合，它可以存储任何可序列化对象。否则，offset 会在每次回发之间恢复为初始值。

要修改 offset，可以使用名为 Cycle() 的方法：

```csharp
public void Cycle()
{
    offset = ++offset;
}
```

此方法只会递增视图状态中保存的 offset 值。

最后要介绍的，或许是任何自定义控件最重要的方法重写——Render()。在此处输出 HTML，因此实现起来可能非常复杂。如果要考虑所有可能查看控件的浏览器，以及可能影响呈现的所有变量，这个方法可能会变得很长。幸运的是，对于此示例，实现起来相当简单：

```csharp
protected override void Render(HtmlTextWriter output)
{
    string text = Text;
    for (int pos = 0; pos < text.Length; pos++)
    {
        int rgb = colors[(pos + offset) % colors.Length].ToArgb() & 0xFFFFFF;
        output.Write(string.Format(
            "<font color=\"#{0:X6}\">{1}</font>", rgb, text[pos]));
    }
}
```

此方法可以访问输出流，以显示控件内容。只有以下两种情况下，你才不需要实现此方法：

- 设计没有视觉表示的控件（通常称为组件）时
- 从现有控件派生，且不需要更改其显示特性时

自定义控件还可以公开自定义方法、引发自定义事件，并响应子控件（如果有）。对于 RainbowLabel，无须考虑这些内容。

接下来，需要添加一个名为 Default.aspx 的网页，并添加代码来查看控件并调用 Cycle()，如下所示：

```
<%@ Register TagPrefix="pcs" Namespace="PCSCustomWebControls" %>

...

<form id='form1' runat='server'>
<div>
<pcs:RainbowLabel runat="server" ID="rainbowLabel1"
Text="彩虹色标签！" />
<asp:Button runat="server" ID="cycleButton" Text="循环颜色"
OnClick="cycleButton_Click" />
</div>
</form>
```

