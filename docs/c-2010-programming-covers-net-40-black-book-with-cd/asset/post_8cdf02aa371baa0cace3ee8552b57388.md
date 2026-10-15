
Noteworthy public properties of the Calendar class are listed in Table 14.24:

| Property | Description |
|---|---|
| Caption | Obtains or sets a text value that is rendered as a caption for the Calendar control |
| CaptionAlign | Obtains or sets the alignment of the text that is rendered as a caption for the Calendar control |
| CellPadding | Obtains or sets the number of space between the data of a cell and the cell's border |
| CellSpacing | Obtains or sets the space between cells |
| DayHeaderStyle | Obtains the style properties for the section that displays the day of the week |
| DayNameFormat | Obtains or sets the name format for the days of the week |
| DayStyle | Gets the style properties for the days in the displayed month |
| FirstDayOfWeek | Obtains or sets the day of the week to display in the first day column of the Calendar control |
| NextMonthText | Obtains or sets the text displayed for the next month navigation control |
| NextPrevFormat | Obtains or sets the format of the next and previous month navigation elements in the title section of the Calendar control |
| NextPrevStyle | Obtains the style properties for the next and previous month navigation elements |
| OtherMonthDayStyle | Obtains the style properties for the days on the Calendar control that are not in the displayed month |
| PrevMonthText | Obtains or sets the text displayed for the previous month navigation control |
| SelectedDate | Obtains or sets the selected date |
| SelectedDates | Obtains a collection of System.DateTime objects that represent the selected dates on the Calendar control |
| SelectedDayStyle | Obtains the style properties for the selected dates |
| SelectionMode | Obtains or sets the date selection mode on the Calendar control that specifies whether the user can select a single day, a week, or an entire month |
| SelectMonthText | Obtains or sets the text displayed for the month selection element in the selector column |
| SelectorStyle | Obtains the style properties for the week and the month selector column |
| SelectWeekText | Obtains or sets the text displayed for the week selection element in the selector column |
| ShowDayHeader | Obtains or sets a value indicating whether the heading for the days of the week is displayed |
| ShowGridLines | Obtains or sets a value indicating whether the days on the Calendar control are separated with gridlines |
| ShowNextPrevMonth | Obtains or sets a value indicating whether the Calendar control displays the next and previous month navigation elements in the title section |
| ShowTitle | Obtains or sets a value indicating whether the title section is displayed |
| TitleFormat | Obtains or sets the format for the title section |
| TitleStyle | Obtains the style properties of the title heading for the Calendar control |
| TodayDayStyle | Obtains the style properties for today's date on the Calendar control |
| TodaysDate | Obtains or sets the value for today's date |
| UseAccessibleHeader | Obtains or sets a value that indicates whether to render the table header <th> HTML element for the day headers instead of the table data <td> HTML element |
| VisibleDate | Obtains or sets the date that specifies the month to display on the Calendar control |
| WeekendDayStyle | Obtains the style properties for the weekend dates on the Calendar control |

The next section is the Immediate Solutions section wherein you can see all these standard controls in action.

## Immediate Solutions

### Using the Button Control

When you add a Button control on a Web page, the following code is added to the source code of the Web page:
<asp:Button ID="Button1" runat="server" Text="Button" />

Now, let’s create a Web application named ButtonControl (also available in CD-ROM) to show the working of the Button control. You can add a Button control to a Web page either by dragging and dropping it from the Standard tab of the Toolbox or by double-clicking it in the Toolbox. In these applications, we are setting the Text and ForeColor properties of a Label control at the Click event of the Button control.

> NOTE
> The applications in this chapter are created using the ASP.NET Empty Web Site template in the New Web Site dialog box. After creating the application, you need to add the Default.aspx page to the application.

### Listing 14.1: Showing the Code of the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title> Button Control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label1" runat="server" Font-Bold="True" Font-Underline="True" Text="Button control example showing text on button click event"></asp:Label>
<br />
<br />
<br />
<asp:Button ID="Button1" runat="server" Font-Bold="True" onclick="Button1_Click" Text="Click Me, I will Welcome You !!" />
&nbsp;<br />
<br />
<asp:Label ID="Label2" runat="server"></asp:Label>
</div>
</form>
</body>
</html>
```

Now, add the code, shown in Listing 14.2, in the code-behind file of the Default.aspx page

### Listing 14.2: Showing the code for the Code-behind File of the Default.aspx Page

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
public partial class _Default : System.Web.UI.Page {
protected void Page_Load(object sender, EventArgs e)
{
}
protected void Button1_Click(object sender, EventArgs e)
```

```
<asp:Label ID="Label1" runat="server" Text="Enter Password"></asp:Label>
<br />
<asp:TextBox ID="TextBox2" runat="server" TextMode="Password" Width="172px"></asp:TextBox>&nbsp; &nbsp;<br />
<asp:TextBox ID="TextBox3" runat="server" Width="173px"></asp:TextBox><br />
</div>
</form>
</body>
</html>
```

# NOTE

The SingleLine TextMode property is a default property of the TextBox control and does not appear in the Default.aspx page.

Now, add the code, shown in Listing 14.4, in the code-behind file of the Default.aspx page for the TextBox controls:

### Listing 14.4: Showing the Code for the Code-behind File of the Default.aspx Page

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
public partial class _Default : System.Web.UI.Page {
    protected void Page_Load(object sender, EventArgs e)
    {
    }
    protected void Button1_Click(object sender, EventArgs e)
    {
        TextBox1.Text = "You have clicked the button";
        TextBox4.Text = "This is a multi line textbox. This is a multi line textbox. This is a multi line textbox. This is a multi line textbox.";
        TextBox3.Text = TextBox2.Text;
    }
}
```

Now, run the application by pressing the F5 key. The output after clicking the Click me button is shown in Figure 14.2:

![](img/e073a4882197be4ab61103cbe0bcb394_719_0.png)

### Figure 14.2: Showing the Types of TextBox Controls

### Using the Label Control

When you add a Label control on a Web page, the following code is added to the source code of the Web page:

```
<asp:Label ID="Label1" runat="server" Text="Label1"></asp:Label>
```

Now, let's create a Web application named LabelControl (also available in CD-ROM) to show the working of the Label control. You can add a Label control to a Web page either by dragging and dropping it from the Standard tab of the Toolbox or by double-clicking it in the Toolbox. In these applications, we are setting the Text and BackColor properties of a Label control at the Page_Load event. Listing 14.5 shows the code of Default.aspx page for the Label controls:

### Listing 14.5: Showing the Code of the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Label Control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label1" runat="server" Text="Example showing some of the properties of the Label Control" Font-Bold="True" Font-Underline="True"></asp:Label>
<br />
<br />
<asp:Label ID="Label3" runat="server"></asp:Label>
<br />
<br />
<asp:Label ID="Label4" runat="server"></asp:Label>
<br />
</div>
</form>
</body>
</html>
```

Now, add the code, shown in Listing 14.6, in the code-behind file of the Default.aspx page:

### Listing 14.6: Showing the Code of the Code-behind File of the Default.aspx Page

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        Label3.Text = "Welcome to the world of ASP.NET 4.0";
        Label4.Text = "I have Olive Color";
        Label4.BackColor = System.Drawing.Color.Olive;
    }
}
```
