

## 清单 10.2（续）

```xml
<label>State:</label>
<asp:DynamicControl runat="server" DataField="Region"
    OnInit="DynamicControl_Init"/>
<label>Zip:</label>
<asp:DynamicControl runat="server" DataField="PostalCode"
    OnInit="DynamicControl_Init"/>
</fieldset>
```

请注意，这里并不是在标记中为每个 DynamicControl 指定 Mode 属性，而是使用一个名为 DynamicControl_Init 的方法来处理所有 DynamicControl 实例的 Init 事件。清单 10.3 显示了定义此方法的代码隐藏文件。DynamicControl_Init 方法依赖其第一个参数 sender 来确定需要初始化的 DynamicControl 实例，然后将该控件的 Mode 属性设置为实体模板自身的 Mode 属性值。

## 清单 10.3 多模式客户实体模板（代码隐藏）

```csharp
using System;
using System.Web.DynamicData;

namespace WebApplication.DynamicData.EntityTemplates
{
    public partial class CustomerEntityTemplate : EntityTemplateUserControl
    {
        protected void InitDynamicControl(object sender, EventArgs e)
        {
            var dynamicControl = (DynamicControl)sender;
            dynamicControl.Mode = this.Mode;
        }
    }
}
```

新的多模式 Customers 实体模板比旧的 Edit 模式实体模板略复杂一些，后者不需要在代码隐藏中编写任何逻辑。然而，这种方法消除了之前使用两个独立模式特定模板时存在的标记重复，使得自定义实体模板的创建和维护更具吸引力。但有一个问题——它不能立刻生效。

## 动态模板

不幸的是，图 5.4 所示的动态数据用于查找实体模板的算法选择了动态 Edit 模式模板 Default_Edit.ascx，即使 Customer 实体可能存在自定义的多模式实体模板。事实证明，动态实体模板与最初版本的 Customer 实体模板存在同样的代码重复问题，你可以用完全相同的方法解决。清单 10.4 显示了动态 Edit 模式模板的标记。

## 清单 10.4 编辑模式动态实体模板（标记）

```
<%@ Control Language="C#" CodeBehind="Default_Edit.ascx.cs" Inherits="WebApplication.DynamicData.EntityTemplates.DefaultEditEntityTemplate" %>
<table class="DDDetailsTable">
<asp:EntityTemplate runat="server" ID="entityTemplate">
<ItemTemplate>
<tr>
<td class="DDLightHeader">
<asp:Label runat="server" OnInit="Label_Init" OnPreRender="Label_PreRender"/>
</td>
<td>
<asp:DynamicControl runat="server" ID="DynamicControl" Mode="Edit" OnInit="DynamicControl_Init" />
</td>
</tr>
</ItemTemplate>
</asp:EntityTemplate>
</table>
```

如你所见，Default_Edit 实体模板把 DynamicControl 实例的 Mode 属性硬编码为 Edit 值。Default_Insert 实体模板硬编码为 Insert 值，而 Default（只读）模板则保留默认的 ReadOnly 值。除此之外，这三个动态模板之间没有其他显著差异，你可以用清单 10.5 中显示的单一多模式模板替换它们。

## 清单 10.5 多模式动态实体模板（标记）

```
<%@ Control Language="C#" CodeBehind="Default.ascx.cs" Inherits="WebApplication.DynamicData.EntityTemplates.DefaultEntityTemplate" %>
<table class="DDDetailsTable">
<asp:EntityTemplate runat="server" ID="entityTemplate">
<ItemTemplate>
<tr>
<td class="DDLightHeader">
<asp:Label runat="server" OnInit="Label_Init" OnPreRender="Label_PreRender" />
</td>
<td>
<asp:DynamicControl runat="server" ID="dynamicControl"
```

## 清单 10.5（续）

```
OnInit="DynamicControl_Init" />
</td>
</tr>
</ItemTemplate>
</asp:EntityTemplate>
</table>
```

请注意，这个新版本与清单 10.4 中显示的先前版本几乎相同。DynamicControl 中删除了硬编码的 Mode 属性，但 DynamicControl_Init 事件处理程序已经就位，因为动态实体模板已经需要以编程方式初始化 DynamicControl 实例的另一个属性——DataField 属性。

清单 10.6 显示了动态多模式实体模板的代码隐藏。粗体表示这个新实现与原始 Default_Edit 和 Default_Insert 实体模板的代码隐藏之间唯一显著的区别。

## 清单 10.6 多模式动态实体模板（代码隐藏）

```
using System;
using System.Collections.Generic;
using System.Web.DynamicData;
using System.Web.UI.WebControls;

namespace WebApplication.DynamicData.EntityTemplates
{
    public partial class DefaultEntityTemplate : EntityTemplateUserControl
    {
        private MetaColumn currentColumn;

        protected override void OnLoad(EventArgs e)
        {
            IEnumerable<MetaColumn> scaffoldColumns = this.Table.GetScaffoldColumns(
                this.Mode, this.ContainerType);
            foreach (MetaColumn column in scaffoldColumns)
            {
                this.currentColumn = column;
                NamingContainer container = new NamingContainer();
                this.entityTemplate.ItemTemplate.InstantiateIn(container);
                this.entityTemplate.Controls.Add(container);
            }
        }

        protected void Label_Init(object sender, EventArgs e)
        {
```

以便包含人类可读的属性名称，而不是它们内部的 Pascal 大小写形式的值。清单 10.7 显示了一个示例，说明如何通过将 DisplayAttribute 应用于实体属性来指定显示名称。

## 清单 10.7 客户实体数据注释

```
using System.ComponentModel.DataAnnotations;

namespace DataModel
{
    [MetadataType(typeof(Customer.Metadata))]
    partial class Customer
    {
        public abstract class Metadata
        {
            [Display(Name = "Name")]
            public object ContactName { get; set; }

            [Display(Name = "ID")]
            public object CustomerID { get; set; }
        }
    }
}
```

在当前实现中，通过数据注释指定的显示名称与模板标记中硬编码的名称相匹配。然而，在现实世界的应用程序中，随着开发人员不断学习业务领域，术语发生变化是很常见的。当特定属性的显示名称发生变化时，需要更新所有硬编码了该名称的位置。动态实体模板通过根据列元数据生成标签来解决这个问题，因此显示名称只需在数据模型中指定一次。然而，在自定义实体模板中使用相同的方法会有问题，因为内置的 Label 控件不能直接与特定的 MetaColumn 关联。

这个问题可以通过一个简单的控件 UnleashedLabel 来解决，它包含在本书附带的示例 Unleashed.DynamicData 项目中。该控件继承自 Label 类，与 DynamicControl 和 DynamicHyperLink 类似，定义了一个名为 DataField 的属性，用于保存需要由模板呈现显示名称的实体属性的名称。你可以在模板标记中指定 DataField，控件会在运行时找到相应的 MetaColumn 并呈现其 DisplayName。因此，与其像这样硬编码客户名称：`<label>Name</label>`，你可以在模板标记中这样实现：`<unl:UnleashedLabel runat="server" DataField="ContactName" />`。

## 扩展 DynamicControl

到目前为止，你必须为每个多模式实体模板中的每个 DynamicControl 实例指定 Init 事件处理程序。对于自定义模板，尤其是较复杂的模板，这不仅繁琐且容易出错，还会增加模板标记的体量，降低其可读性。

为了让自定义多模式模板的实现更加容易，UnleashedControl（位于示例 Unleashed.DynamicData 项目中）扩展了内置 DynamicControl，以根据父实体模板的模式来设置自身的 Mode 属性。不是使用以下标记：

```
<asp:DynamicControl runat="server" DataField="ContactName" OnInit="DynamicControl_Init"/>
```

你只需简单地编写：

```
<unl:UnleashedControl runat="server" DataField="ContactName"/>
```

而不必担心指定 Init 事件处理程序。清单 10.9 包含了 UnleashedControl 的完整源代码。

## 清单 10.9 UnleashedControl 实现

```
using System;
using System.Web.DynamicData;
using System.Web.UI.WebControls;

namespace Unleashed.DynamicData
{
    public class UnleashedControl : DynamicControl
    {
        protected override void OnInit(EventArgs e)
        {
            if (this.Mode == DataBoundControlMode.ReadOnly)
            {
                var entityTemplate = this.TemplateControl as EntityTemplateUserControl;
                if (entityTemplate != null)
                {
                    this.Mode = entityTemplate.Mode;
                }
            }
            base.OnInit(e);
        }
    }
}
```

