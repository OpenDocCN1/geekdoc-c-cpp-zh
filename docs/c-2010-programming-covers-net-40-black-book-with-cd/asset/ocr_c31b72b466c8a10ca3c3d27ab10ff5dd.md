```
```html
<head id="Head1" runat="server">
    <title>LINQ to XML</title>
</head>
<body>
    <form id="Form" runat="server">
        <div id="header">
            <h1>
                C# 2010 Black Book
            </h1>
        </div>
        <div id="content">
            <div class="itemContent">
                <asp:ListBox ID="ListBox1" runat="server" Height="236px"
                    style="margin-left: 97px; margin-top: 53px"
                    Width="398px"></asp:ListBox>
                <br />
                <asp:Button ID="Button1" runat="server" onclick="Button1_Click"
                    style="margin-left: 126px" Text="Display" Width="136px" />
            </div>
        </div>
    </form>
</body>
</html>
```
```

After modifying the code in the source file, change the code in the code-behind file of the Default.aspx page, as shown in Listing 27.7:

**Listing 27.7:** Showing the Code for the Code-Behind File of the Default.aspx Page

```
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Xml.Linq;

public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {

    }
    protected void Button1_Click(object sender, EventArgs e)
    {
        try
        {
            XElement employees = XElement.Parse
            (
                @"<employees>
                    <employee>
                        <ID>E001</ID>
                        <name>Ram</name>
                        <designation>Writer</designation>
                    </employee>
                    <employee>
                        <ID>E002</ID>
                        <name>Harry</name>
                        <designation>Manager</designation>
                    </employee>
                    <employee>
```
```