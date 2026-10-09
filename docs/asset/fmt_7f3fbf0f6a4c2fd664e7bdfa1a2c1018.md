
由于你希望立即计算账单，在选择任何 `RadioButton` 控件的时刻，将所有 `RadioButton` 控件的 `AutoPostBack` 属性设置为 `true`。为了在从任一组或两组中选择任一 `RadioButton` 控件时计算并显示账单，请修改 `Default.aspx.cs` 文件中的代码，使其如代码列表 18.8 所示。只有加粗的代码与你在代码列表 18.7 中看到的相同。

## 酒店预订

| 项目 | 价格 |
| :--- | :--- |
| Airport Pickup | $20 |
| WiFi | $10 |
| Buffet Food | $15 |
| Queen Bed | $125 |
| King Bed | $150 |
| Standard Room | $125 |
| Deluxe Room | $150 |
| Honeymoon Suite | $225 |

图 18.18

显示两组 `RadioButtons` 的屏幕。当你从每个组中选择任何 `RadioButton` 时，账单会相应的显示。

## 使用 LISTBOX 控件

你可以使用 `ListBox` 控件在有限的空间内显示一组项目。它不仅能在空间内显示更多项目，还允许用户进行多选。表 18.7 简要描述了 `ListBox` 控件的常用属性。

### 18.7 ListBox 的常用属性

| 属性 | 说明 |
| :--- | :--- |
| Items | 返回与控件中的项目对应的 `ListItem` 对象的集合。此属性返回一个 `ListItemCollection` 对象。 |
| Rows | 返回 `ListBox` 中一次显示的项目数。如果列表包含的行多于可显示的行数，则会自动添加滚动条。 |
| SelectedItem | 返回当前选中项的 `ListItem` 对象，或者如果选择了多个项，则返回索引最低的项的 `ListItem` 对象。 |
| SelectedIndex | 返回当前选中项的索引，如果在 `ListBox` 中选择了多个项，则返回第一个选中项的索引。如果 `ListBox` 中未选择任何项，此属性的值为 -1。 |
| SelectedValue | 返回当前选中项的值，如果在 `ListBox` 中选择了多个项，则返回第一个选中项的值。如果未选择任何项，此属性的值为空字符串。 |
| SelectionMode | 决定 `ListBox` 允许单选（Single）还是多选（Multiple）。 |

![](img/3ca47f8f6f5560f07650d3563e2f2c05_606_0.png)

**图 18.19**

`ListBox` 控件的外观。

经微软许可使用。

你将显示代表访问酒店目的的选项。换句话说，你将通过 `ListBox` 显示“旅游”和“商务”等选项。

### 使用 ListBox 控件 59

`ListBox`（列表框）控件。用户可以从可用选项列表中选择一个，以指示其访问目的。

将 `Label` 控件的 `Text` 属性设置为“Purpose of visit”（访问目的）。要通过 `ListBox` 控件显示不同的选项，请在设计窗口中选择该控件，然后在属性窗口中选择 `Items` 属性。在图 18.20 所示的 `ListItem Collection Editor` 对话框中，通过点击 `Add` 按钮添加 `Tourism`（旅游）、`Business`（商务）、`Education`（教育）、`Research`（研究）和 `Other`（其他）项目。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_607_0.png)

**图 18.20**

在 `ListBoxBox` 控件中使用 `ListItem Collection Editor` 添加项目并指定其值。

经微软许可使用。

将 `ListBox` 控件的 `ID` 设置为 `listboxPurpose`。同时，将 `AutoPostBack` 属性的值设为 `true`。你可以将 `SelectionMode` 设置为 `Single`（单选）或 `Multiple`（多选）模式。最初，将 `SelectionMode` 属性保持为默认值（Single），如图 18.21 所示。

### 第 18 章 .NET Web 应用程序开发

![](img/3ca47f8f6f5560f07650d3563e2f2c05_608_0.png)

图 18.21

设置 `Listbox` 控件的 `ID`、`AutoPostBack` 和 `SelectionMode` 属性。

经微软许可使用。

在 Web 表单上拖放一个 `Label` 控件，并将其 `ID` 属性设置为 `lbl1Purpose`。此时 Web 表单显示如图 18.22 所示。

## 使用 ListBox 控件

![](img/3ca47f8f6f5560f07650d3563e2f2c05_609_0.png)

图 18.22

带有 `ListBox` 控件的 Web 表单。

经微软许可使用。

当用户从 `ListBox` 控件中选择任何选项时，你希望让选中的项目通过 `Label` `lbl1Purpose` 显示，请在设计窗口中双击 `ListBox` 控件，并在打开的代码后置文件中输入以下语句：

```
protected void listBoxPurpose_SelectedIndexChanged(object sender, EventArgs e)
{
    lbl1Purpose.Text = "Your purpose of visit is "+listBoxPurpose.Text;
}
```

上述代码通过 `Label` 控件显示从 `ListBox` 控件中选的文本，如图 18.23 所示。

## 酒店房间预订

- 机场接机 $20
- WiFi $10
- 自助餐 $15
- 双人床 $125
- 大床 $150
- 标准房 $125
- 豪华房 $150
- 蜜月套 $225

访问目的

旅游 商务 教育 研究

账单 [275] \ 您的访问目的是：教育

图 18.23

从 `ListBox` 控件中选定的选项通过 `Label` 控件显示。经微软许可使用。

要从 `ListBox` 控件中选择多个项目，请将其 `SelectionMode` 属性设置为 `Multiple`。要显示从 `ListBox` 控件中选出的所有选项，在设计窗口中双击并修改代码如下：

```
protected void listBoxPurpose_SelectedIndexChanged(object sender, EventArgs e)
{
    String str = "";
    foreach (ListItem purpose in listBoxPurpose.Items)
    {
        if (purpose.Selected == true)
        {
            str = str + purpose.Text + " ";
        }
    }
    lblPurpose.Text = "Your purpose of visit is "+str;
}
```

如前述代码所示，在 `ListItem` 对象 `purpose` 的帮助下，对 `ListBox` 控件的每个 `Items` 属性项进行了测试。你创建了字符串变量 `str`。当 `purpose` 项目被选中时，`str` 就会拼接该目的文本和空格。最后，通过 `lblPurpose` 控件显示访问目的。如图 18.24 所示。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_607_0.png)

**图 18.24**

`ListBox` 控件中的项目显示。

# 第 18 章 .NET 中的 Web 应用程序开发

![](img/3ca47f8f6f5560f07650d3563e2f2c05_616_0.png)

图 18.30

设置 `HyperLink` 控件的 `Text` 和 `NavigateUrl` 属性。

经 Microsoft 许可使用。

运行应用程序后，你将获得一个文本为 "Payment Info"（支付信息）的链接（与图 18.28 [左侧] 相同）。当你点击 "Payment Info" 链接时，页面将从当前的 `Default.aspx` Web 表单导航到 `Checkout.aspx` Web 表单。

除了文本外，你还可以让图像充当超链接。要实现这一点，你需要向你的网站添加一些图像。在资源生成管理器（Explorer）窗口中右键点击 `HotelReservApp`，选择 `Add`（添加）、`New Folder`（新建文件夹）。系统会提示输入新添加文件夹的名称。为新添加的文件夹命名为 `images`。将你任何想要显示为超链接的图像复制并使用到网站的 `images` 文件夹中。假设复制到 `images` 文件夹的图像文件名为 `mastercard.jpg`，设置 `ImageUrl`、`ImageHeight` 和 `ImageWidth` 属性，如图 18.31 所示。`NavigateUrl` 属性应指向同一个 Web 表单 `Checkout.aspx`。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_617_0.png)

**图 18.31**

设置 `Hyperlink` 控件的 `ImageUrl`、`ImageHeight` 和 `ImageWidth` 属性。

经 Microsoft 许可使用。

当你设置 `ImageUrl` 属性后，文本 "Payment Info" 将被指定的图像替换（见图 18.32 [左侧]）。换句话说，图像不再充当超链接。

当你点击图像时，页面将从当前 Web 表单导航到 `Checkout.aspx` Web 表单，如图 18.32（右侧）所示。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_618_0.png)

图 18.32 (左侧) 超链接以图像格式出现 (右侧) 点击图像后导航到目标 Web 表单。经 Microsoft 许可使用。

你还可以根据条件动态更改链接文本或目标页面。此外，你可以使用数据绑定为链接指定目标 URL（如果需要，还可以指定随链接传递的参数）。

## 注意

当用户点击 `HyperLink` 控件时，它不会在服务器代码中引发事件。相反，导航是从当前 Web 表单到 `NavigateUrl` 属性中指定的表单进行的。

还有一个名为 `ImageButton` 的控件，它显示图像并在被点击时产生导航。接下来将介绍它。

# 使用 IMAGEBUTTON 控件

`ImageButton` 控件显示一个可点击的图像。你可以使用该控件显示一个在点击时执行所需操作的图像。图像还可以执行从当前 Web 表单到所需 Web 表单的导航。图 18.33 显示了 `ImageButton` 控件。

```
asp:imageButton#ImageButton1
```

图 18.33

`ImageButton` 控件。

经 Microsoft 许可使用。

以下是使用 `ImageButton` 控件时常用的两个属性：

- `PostBackUrl`——用于指定你想要导航到的 Web 表单路径。
- `ImageUrl`——用于指定你想通过 `ImageButton` 控件显示的图像文件名。该图像需要存在网站的 `images` 文件夹中。

假设你想导航到 `Checkout.aspx` Web 表单并在 `PostBackUrl` 属性中设置其名称。要显示图像，将图像文件名 `contactus.jpg` 复制到网站的 `images` 文件夹中。之后，设置 `ImageUrl` 属性，如图 18.34 所示。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_620.png)

| 属性 | 描述 |
| :--- | :--- |
| PostBackUrl | 用于指定你想要导航到的 Web 表单路径。 |
| ImageUrl | 用于指定你想通过 ImageButton 控件显示的图像文件名。该图像需要存在网站的 images 文件夹中。 |

假设你想导航到 `Checkout.aspx` Web 表单并在 `PostBackUrl` 属性中设置其名称。要显示图像，将图像文件名 `contactus.jpg` 复制到网站的 `images` 文件夹中。之后，设置 `ImageUrl` 属性，如图 18.34 所示。

| 属性 | 描述 |
| :--- | :--- |
| PostBackUrl | 用于指定你想要导航到的 Web 表单路径。 |
| ImageUrl | 用于指定你想通过 ImageButton 控件显示的图像文件名。该图像需要存在网站的 images 文件夹中。 |

图 18.34

设置 `ImageUrl` 属性以显示图像。

## 第 18 章在 .NET 中开发 Web 应用程序

你将创建一个服务，用于计算其提供的三个数字的平均值。如所预期，你需要定义一个声明此任务的服务合约（接口）。你将使用现有的接口 `IService.cs` 来此此。修改 `IService.cs` 使其显示如列表 18.9 所示。

## 列表 18.9 IService1.cs 程序代码

```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.Serialization;
using System.ServiceModel;
using System.ServiceModel.Web;
using System.Text;

namespace WCFAvgServiceApp
{
    [ServiceContract]
    public interface IService1
    {
        [OperationContract]
        double GetAverage(int valueOne, int valueTwo, int valueThree);
    }
}
```

你可以看到在服务文件中，你定义了一个服务合约和一个操作合约。服务合约定义了整个服务，而操作合约定义了服务上提供的各种方法。服务合约通过在类上应用包裹在方括号中的 `ServiceContract` 特性来定义。你想要暴露的服务的每个方法都用 `OperationContract` 特性标记。`GetAverage` 就是你想要暴露并供客户端应用程序使用的方法。

## 注意

> 接口通常被称为服务合约，对应的方法被称为操作合约。

在接口声明之后，现在是时候编写服务实现代码了。打开服务实现文件 `Service1.svc` 并为 `GetAverage` 方法（在 `IService.cs` 文件中声明）定义代码。修改 `Service1.svc` 使其显示如列表 18.10 所示。

## 使用 WCF 609

## 列表 18.10 Service1.cs 文件程序代码

```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.Serialization;
using System.ServiceModel;
using System.ServiceModel.Web;
using System.Text;

namespace WCFAvgServiceApp
{
    public class Service1 : IService
    {
        public double GetAverage(int valueOne, int valueTwo, int valueThree)
        {
            double result = 0;
            try
            {
                result = (valueOne + valueTwo + valueThree) / 3;
            }
            catch (Exception Ex)
            {
                throw new FaultException(new FaultReason(Ex.Message));
            }
            return result;
        }
    }
}
```

你可以看到 `GetAverage` 被定义为接收三个整数参数：`valueOne`、`valueTwo` 和 `valueThree`。计算并返回三个传入参数的平均值。如果在计算平均值期间发生错误，将抛出异常。

要测试 WCF 服务，按 `F5`。将显示 WCF Test Client 对话框以加载服务。在 WCF Test Client 对话框中，双击 `IService` 节点下的 `GetAverage()` 方法。显示 `GetAverage` 表，如图 18.38 所示。在 `Request` 框中，选择 `Value` 字段并输入三个值。然后点击 `Invoke` 按钮。如果显示安全警告对话框，点击 `OK`。结果将显示在 `Response` 框中。

## 第 18 章在 .NET 中开发 Web 应用程序

![](img/3ca47f8f6f5560f07650d3563e2f2c05_626_0.png)

**图 18.38**

在 WCF Test Client 中提供的 `GetAverage()` 方法的三个参数的值。

经微软许可使用。

观察 `Response` 框中的值以查看结果是否正确。为了让客户端能够访问服务，它需要是公开的，因此你必须发布它。在启动发布程序之前，通过选择文件（File）、退出（Exit）关闭 WCF Test Client 对话框。

要开始发布服务，在解决方案管理器中右键点击应用程序并选择发布（Publish）选项。打开发布 Web 对话框。第一步是创建发布配置文件，因此从下拉列表中选择新配置文件（New Profile）来创建一个新配置文件（见图 18.39）。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_627_0.png)

**图 18.39**
