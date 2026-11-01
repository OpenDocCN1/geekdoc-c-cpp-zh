# LISTING 11.2 Modified Enumeration Field Template (Markup)

```
<%@ Control Language="C#" CodeBehind="Enumeration.ascx.cs" Inherits="WebApplication.DynamicData.FieldTemplates.EnumerationField" %>
<asp:Literal runat="server" ID="literal" Text="<%# FieldValueString %>" />
```

Overall, the implementation of the Enumeration field template becomes much simpler because you are mostly removing unnecessary code. The new version of the code-behind is shown in Listing 11.3.

# LISTING 11.3 Modified Enumeration Field Template (Code-Behind)

```
using System.Web.UI;
using Unleashed.DynamicData;

namespace WebApplication.DynamicData.FieldTemplates
{
    public partial class EnumerationField : UnleashedEnumerationFieldTemplate
    {
        public override Control DataControl
        {
            get { return this.literal; }
        }
    }
}
```

Figure 11.5 shows how the modified version of the Enumeration field template looks on a page; as you can see, the display name of the EmployeeType is shown, not its internal (PascalCased) name.

![](bbox=[0.12, 0.81, 0.38, 0.9])

FIGURE 11.5 Extended Enumeration field template.

Enum types help to reduce complexity of entity models and improve performance of the application. This simple extension to the built-in Enumeration field templates to support display name annotations eliminates one of the most common reasons why developers introduce lookup tables in their applications. This allows you to take full advantage of enums today and prepare for the upcoming 4.5 release of the Entity Framework where you get first class support in both Entity Designer and LINQ to Entities.