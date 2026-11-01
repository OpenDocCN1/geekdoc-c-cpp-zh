
Web 应用程序项目。图 10.4 显示了使用新字段模板生成的客户编辑页面的示例；清单 10.11 显示了其标记。

![](img/11b373b78859e17d318fd76939a0df9d_343_0.png)

## 图 10.4 使用自定义 State 字段模板的网页。

## 清单 10.11 State_Edit 字段模板（标记）

```
<%@ Control Language="C#" CodeBehind="State_Edit.ascx.cs" Inherits="WebApplication.DynamicData.FieldTemplates.StateEditField" %>

<asp:DropDownList ID="dropDownList" runat="server" />

<asp:RequiredFieldValidator runat="server" ID="requiredFieldValidator" ControlToValidate="dropDownList" Enabled="false" />
<asp:DynamicValidator runat="server" ID="dynamicValidator" ControlToValidate="dropDownList" />
```

虽然此自定义字段模板是专门为 Region 列构建的，但仍然很重要遵循通用字段模板使用的模式，并创建 RequiredFieldValidator 和 DynamicValidator 控件来验证用户在 DropDownList 中选择的值。你希望尽可能将业务逻辑排除在自定义模板之外。一方面，这使得用户界面的实现更简单——只需在模板标记中放置适当的验证器，让 Dynamic Data 处理其余部分。另一方面，将业务逻辑集中在数据模型中，并通过数据注释和在实体类中实现的自定义代码进行处理，有助于保持其可维护性和可测试性。

正如你所期望的那样，State_Edit 字段模板中的大部分繁重工作都在其代码隐藏中完成，如清单 10.12 所示。

## 清单 10.12 State_Edit 字段模板（代码隐藏）

```
using System;
using System.Collections.Specialized;
using System.Web.DynamicData;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace WebApplication.DynamicData.FieldTemplates
{
    public partial class StateEditField : FieldTemplateUserControl
    {
        public override Control DataControl
        {
            get { return this.dropDownList; }
        }

        private static readonly string[] states = new string[]
        {
            "AL", "AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA",
            "HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD",
            "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ",
            "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC",
            "SD", "TN", "TX", "UT", "VT", "VA", "WA", "WV", "WI", "WY"
        };

        protected override void OnInit(EventArgs e)
        {
            base.OnInit(e);

            this.dropDownList.Items.Add(new ListItem(string.Empty));
            foreach (string state in states)
                this.dropDownList.Items.Add(new ListItem(state));

            this.SetupValidator(this.requiredFieldValidator);
            this.SetupValidator(this.dynamicValidator);
        }

        protected override void OnDataBinding(EventArgs e)
        {
            base.OnDataBinding(e);
            if (this.dropDownList.Items.FindByValue(this.FieldValueEditString) != null)
                this.dropDownList.SelectedValue = this.FieldValueEditString;
        }

        protected override void ExtractValues(IOrderedDictionary dictionary)
        {
            dictionary[this.Column.Name] =
                this.ConvertEditedValue(this.dropDownList.SelectedValue);
        }
    }
}
```

OnInit 方法使用美国州缩写的静态数组填充 DropDownList 控件中的项目列表，并通过调用 FieldTemplateUserControl 基类提供的 SetupValidator 方法来初始化验证器。OnDataBinding 方法根据数据库中先前存储的州值提供 DropDownList 的初始选择，而 ExtractValues 方法在保存客户实体到数据库时，将用户选择的新值返回给数据源控件。

<asp:DynamicControl runat="server" DataField="Region" UIHint="State" />

创建了新的自定义字段模板后，你现在可以按刚才所示修改 Customer 实体模板，以便将其用于 Region 属性，而不是默认字段模板。

> **NOTE**
>
> DynamicControl 类的 UIHint 属性的值不应包含字段模板名称中使用的 _Edit 后缀。如第 4 章所述，Dynamic Data 在查找字段模板时会将此后缀自动添加到 UIHint 值，如果你将 UIHint 设置为 State_Edit，它将查找名为 State_Edit_Edit 的字段模板。

## 在字段模板之间实现交互

不幸的是，当你开始使用新的 State 字段模板时，很快就会发现它对国际客户并不适用。Northwind Traders 也与欧洲的客户开展业务，但只有美国和加拿大在邮寄地址中使用州，或更准确地说，地区。此外，对于美国和加拿大，你还需要用户只能看到特定国家/地区对应的地区。换句话说，Customer 实体的 Region 属性的字段模板必须以某种方式与 Country 属性的字段模板协同工作，以提供所需的用户体验。

你可以通过将自定义字段模板从 State_Edit 重命名为 Region_Edit 来开始解决此问题，以更准确地反映它不仅用于美国客户，也用于其他国家的客户。由于地区列表不再是静态的，你无法假装知道所有国家/地区的所有可能地区，需要改回使用 TextBox 作为数据输入控件。然而，为了让最常见的国家/地区的数据输入更轻松，你可以使用 AJAX 控件工具包中的 AutoCompleteExtender，根据用户输入的国家/地区为其建议众所周知的地区列表。

```
<asp:TextBox ID="textBox" runat="server" Text="<%# FieldValueEditString %>"/>
<ajax:AutoCompleteExtender ID="autoCompleteExtender" runat="server"
    TargetControlID="textBox" ServicePath="/RegionCompletionService.svc"
    ServiceMethod="GetCompletionList" />
```

AutoCompleteExtender 需要一个 Web 服务方法来获取建议值的列表。此 Web 服务在清单 10.13 中显示，定义了单个方法 GetCompletionList，该方法将由 AutoCompleteExtender 根据 ServicePath 和 ServiceMethod 属性生成的客户端 JavaScript 代码调用。虽然方法名称本身在标记中配置，但参数的名称和顺序必须与 AutoCompleteExtender 实现期望的完全匹配。特别是，prefixText 参数接收用户在 Region 文本框中输入的当前值，count 指定应返回的匹配项数量，而 contextKey 将是用户在 Country 字段中输入的值。

## 清单 10.13 RegionCompletionService 实现

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.ServiceModel;

namespace WebApplication
{
    [ServiceContract]
    public class RegionCompletionService
    {
        private static readonly Dictionary<string, string[]> regionsByCountry =
            new Dictionary<string, string[]>(StringComparer.InvariantCultureIgnoreCase)
        {
            { "Canada",
                new[] {
                    "ON", "QC", "NS", "NB", "MB", "BC", "PE", "SK", "AB", "NL",
                    "NT", "UT", "NU"
                }
            },
            { "USA",
                new[] {
                    "AL", "AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA",
                    "HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD",
                    "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ",
                    "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC",
                    "SD", "TN", "TX", "UT", "VT", "VA", "WA", "WV", "WI", "WY"
                }
            }
        };

        [OperationContract]
        public string[] GetCompletionList(
            string prefixText, int count, string contextKey)
        {
            var country = contextKey ?? string.Empty;
            string[] regions;
            if (regionsByCountry.TryGetValue(country, out regions))
            {
                var ignoreCase = StringComparison.InvariantCultureIgnoreCase;
                return regions
                    .Where(r => r.StartsWith(prefixText, ignoreCase))
                    .Take(count)
                    .ToArray();
            }
            return new string[0];
        }
    }
}
```

RegionCompletionService 使用 Dictionary 对象为每个已知国家/地区存储地区列表。GetCompletionList 方法在字典中执行查找以找到给定国家/地区的地区数组，并仅返回以用户输入的前缀开头的地区。字典查找和前缀过滤均实现为忽略大小写。

使用 WCF，实现服务只是战斗的一半；端点配置对于允许客户端代码（在本例中为 JavaScript）成功调用服务至关重要。在示例项目中，这是通过在 .SVC 文件的 @ServiceHost 指令中指定 WebScriptServiceHostFactory 来完成的，它负责根据 SVC 文件的位置配置 HTTP 端点并接受由 AutoCompleteExtender 生成的 JSON 格式的方法调用。

## 清单 10.14 RegionCompletionService.svc

```
<%@ ServiceHost Language="C#" Debug="true" Service="WebApplication.RegionCompletionService" CodeBehind="RegionCompletionService.svc.cs" Factory="System.ServiceModel.Activation.WebScriptServiceHostFactory" %>
```
