

# 辅助功能控制特性

大多数 ASP.NET 控件在适用情况下都符合一组特定的无障碍功能列表。其目标是让无障碍编程变得简单，并对用户实用。

- 任何不是由文本组成的元素都应该有一个替代文本选项。例如，所有图像标签都支持 `AlternateText` 属性，该属性会填充 HTML 的 `alt` 标签。网页阅读器将“读出”该标签的内容来代替图像。如果你在网页上添加图像，Visual Studio 会提示你填入替代文本。
- 控件不要求使用样式表或依赖颜色。如果你愿意，可以很容易地从页面中剥离所有信息，以便阅读器或低视力版本的应用程序使用。
- “从用户处获取输入”中的所有输入控件都支持 `TabIndex`，该属性允许用户通过 Tab 键在控件之间切换。对于那些不使用鼠标的用户来说，这是最好的。
- 在 ASP.NET 中，通过 `DefaultFocus` 属性设置表单某部分的默认光标（称为焦点）是非常简单的。使用 `SetFocus` 方法可以轻松地更改。
- 按钮可以使用 `AccessKey` 属性获取键盘等效键。
- 标签和输入控件可以关联，许多阅读器都依赖此项。

# 设计考虑

无障碍的主要设计考虑是使用这些功能。设置替代文本。使用 Tab 索引。设置默认焦点。让你的应用程序对所有人都易于使用。

Visual Studio 2010 中有一个新功能“检查页面无障碍”（Check Page for Accessibility），它可以检查 WCAG 和 Section 508 错误。如果你使用此功能，警告将发布到你的体系生成过程中。

# 构建用户控件

你是否去过一个将三段美国电话显示为三个文本框的网站？你通常会自动在它们之间按 Tab 键，这种结构确保你在每个文本框中的位数完全正确。这是你可以在很多应用程序的每个页面用用到的，对吧？

那个电话号码控件由我们周围已有的东西组成：文本控件、客户端脚本和验证。你只需要将它们组合在一起。

# 构建用户控件 681

你用来以有用方式组合现有控件的技术称为用户控件（User Control），或 ASCX。ASCX 是封装的、易于创建且更易使用的。

# 创建新的电话号码用户控件

为了让你明白我的意思，这里我为你展示如何制作我最喜欢的用户控件——电话号码控件。在这个版本中，它只适用于美国格式，但足够了。它传达了核心点。只需按照以下步骤创建电话号码控件：

- 1. 在本章一直使用的项目中，右键点击项目文件，并选择“添加->新建项”。
- 2. 选择“Web 用户控件”（Web User Control）（参见图 3-9），命名为 `PhoneNumber.ascx`。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_706_0.png)

图 3-9：添加电话号码控件。

控制你的开发体验

- 3. 切换设计视图。
- 4. 将三个文本框拖到设计器中，并相邻排列。如果你想弄得复杂一点，可以在它们之间加上连字符。
- 5. 在属性面板中，将前两个文本框的 `MaxLength` 设置为 3，最后一个设置为 4。这可以防止用户在字段中输入过多的字符。

# 682 构建用户控件

- 6. 右键点击设计器并选择“查看代码”。
- 7. 在代码后（code-behind）中添加一个属性，允许使用该控件的页面获取电话号码。

目标是从控件获取所有内容，将其拼接在一起，进行格式化，并作为公共属性交付。以下是代码：

```
private string _phoneNumber;
public string PhoneNumberValue
{
    get
    {
        _phoneNumber = string.Format("{0}{1}-{2}");
        return _phoneNumber;
    }
}
```

现在我们有了一个控件——就像工具箱中的控件一样——它可以接受分段的电话号码并进行美化格式化。让我们玩玩它吧。

# 使用你的新控件

你会喜欢这个控件的。它的工作方式真的和工具箱中的控件一样。按照以下步骤查看它是如何工作的：

- 1. 右键点击项目，添加一个新的 Web 文件。我将其命名为 `UseThePhoneNumber.aspx`。
- 2. 切换到设计视图。
- 3. 直接从解决方案管理器中将 asc 控件拖到设计表面上。

登登！控件显示得就像普通的文本框一样，但它是经过格式化的。查看图 3-10。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_707_0.png)

- 4. 向表单中添加一个标签和一个按钮。尝试填充控件，点击按钮，并查看格式化后的电话号码。

- 5. 双击按钮以获取点击事件的事件程序。添加一些代码在点击按钮时填充标签，如下所示：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace Custom_3
{
    public partial class UseThePhoneNumber : System.Web.UI.Page
    {
        protected void Button1_Click(object sender, EventArgs e)
        {
            Label1.Text = PhoneNumber1.PhoneNumberValue;
        }
    }
}
```

- 6. 右键点击 ASPX 页面并将其设置为页面。
- 7. 按 `F5` 运行。标签中应该会显示格式化的电话号码。

这是一个非常基础的例子，但你可以看到它是如何使用的。

# 添加自定义控件

超出用户控件范围的是一种可能没人想过的控件。也许你的公司需要一个用代码实现的设备。使用我们在本章中工具构建的服务器控件。不要被骗了——构建服务器控件并非易事。要开始，你需要全新的项目，而不仅仅是一个文件。项目类型是服务器控件，它为我们提供了可以开始的代码，如下：

# 684 添加自定义控件

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Linq;
using System.Text;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace ServerControl
{
    [DefaultProperty("Text")]
    [Control(<{0}:ServerControl runat="server"/></{0}:ServerControl>>
    public class ServerControl : WebControl
    {
        [Bindable(true)]
        [Category("Appearance")]
        [DefaultValue("*")]
        [Localizable(true)]
        public string Text
        {
            get
            {
                String s = (String)ViewState["Text*"];
                return (s == null) ? "*" + this.ID + "*" : s;
            }
            set
            {
                ViewState["Text*"] = value;
            }
        }

        protected override void RenderContents(HtmlWriter output)
        {
            output.Write(Text);
        }
    }
}
```

