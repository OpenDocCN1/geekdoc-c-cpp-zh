
## 664 Getting Some Input from the User

```html
<asp:TableRow runat="server">
  <asp:TableCell runat="server"></asp:TableCell>
  <asp:TableCell runat="server"></asp:TableCell>
  <asp:TableCell runat="server"></asp:TableCell>
</asp:TableRow>
</div>
</form>
<body>
</html>
```

So what's the point of creating tables this way? Well, you can name those rows and cells, and manage them in the code-behind using C#. In all honesty, though, that's not how I recommend doing things.

Tables are good for two things — layout and tabular data. Layout has been superseded by CSS. I recommend you use CSS to lay things out.

For tabular data, tables still work. However, there is a more interesting solution. The GridView (found in the Data section of the Toolbox) is just functional and it is bindable. We chat more about that in the Binding section later.

## Getting Some Input from the User

Acquiring input from the user is one of the most significant processes that Web developers do. Data-active Web is all about interactivity: Web 2.0 is all about interactivity. Getting information from a user is job one.

You can do a lot of things to get input from the user, there is a subset of the controls that is generally considered to be "User Input." You'll use those controls a lot.

### Using text input controls

The most obvious form of collecting data from a user is the text input boxes, as shown in Figure 3-2. In HTML there are three defined controls: the textbox, the password, and the textarea. The TextBox ASP.NET control handles all of those. A TextBox property tells IIS how to render the control.

To use the TextBox control, drag it into the designer from the Toolbox. You can change the property of the control instance — the only other significant element — in the ASP.NET markup, the property panel, or the C code.

The properties that we are most interested in are C:

- **ID:** The name that you use to reference the control in the C# code. It needs to be set first, before you can use the control.

## Getting Some Input from the User 665

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_690_0.png)

Figure 3-2:
The three text inputs, all in a row.

- **TextMode:** This determines the type of text box that gets rendered, as I mentioned.
- **MaxLength:** The maximum number of characters that the user can use in the field. Note that this doesn't work when the TextMode is defined as TextArea.
- **Height and Width:** The size that the text box appears on the page.
- **CssClass:** The style sheet class that the control will be rendered to use. Must be used in conjunction with a style sheet.
- **Enabled:** Marks if the field can be typed in by the user.

In the example 3-1

```csharp
@ Page Language="C#" AutoEventWireup="true" CodeBehind="TextInput.aspx.cs" Inherits="Chapter_3.WebForm" %>

<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0 Transitional//EN" "http://www.w3.org/TR/html1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head>
runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
```

Book VI
Chapter 3
Controlling Your
Development Experience

## 666 Getting Some Input from the User

```html
1 - The TextBox<br />
<asp:TextBox ID="Textbox1" runat="server">The TextBox</asp:TextBox>
<br />
<br />
2. The TextArea<br />
<asp:TextBox ID="Textbox2" runat="server" TextMode="Multiline">The TextArea</asp:TextBox>
<br />
<br />
3. The Password<br />
<asp:TextBox ID="Textbox3" runat="server" TextMode="Password">The Password</asp:TextBox>

</div>
</form>
</body>
</html>
```

In order to set properties in the C# code, I would refer to the ID, as set in the property panel. If I use the defaults (don't do this in real case, make real names for controls), configuring the first text box might look something like this:

```csharp
public partial class WebForm1 : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        TextBox1.MaxLength = 20;
        TextBox1.Height = 22;
        TextBox1.Width = 135;
        TextBox1.Enabled = true;
    }
}
```

### Using single-item selection controls
After collecting text, the most common user-input gathering operation is asking them to choose an item from a list. In HTML, you can do this with check boxes, radio buttons, or drop-down lists. (See Figure 3-3).

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_691_0.png)

**Figure 3-3:**
The single selectors.

## Getting Input from the User 667

ASP.NET provides for all of these items:

- **The Boolean check box:** This is just one single check box where the answer is Yes or No. This is still considered a single item selection even though there is only one item to select from and is usually used to represent a Boolean or in the C# code. It is represented by the `checkbox` control.

- **The radio button list:** Radio buttons are nice because they prevent the user from selecting more than one option while selecting the options. Lists are an interesting beast, because they can be collected. We cover that in the next section, "Binding". This control is radiobuttonlist.

- **The drop-down list:** Represented by the dropdown control, this type of list allows the user to click to see the list, and then click one, which chooses the list. It can also be bound to a collection.

Here is the code for all three. Note that both the dropdown and the radiobutton use the `listitem` control to render the list items.

```aspsharp
@ Page Language="C#" AutoEventWireup="true" CodeBehind="ListItem.aspx.cs Inherits="ListItem3, ListItem">
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN" "http://www.w3.org/TR/html40/html-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta runat="server">
<title>ListItem</title>
</head>
<body>
<form id="form1" runat="server">
  1. The Checkbox br<br />
  <asp:CheckBox ID="Checkbox1" runat="server" />
  <br />
  <br />
  2. The Radio Button List<br />
  <asp:ListBox ID="ListBox1" runat="server">
    <asp:ListItem Item="Item1"</asp:ListItem>
    <asp:ListItem Item="Item2"</asp:ListItem>
    <asp:ListItem Item="Item3"</asp:ListItem>
    <asp:ListItem Item="Item4"</asp:ListItem>
  </asp:ListBox>
  <br />
  3. The DropdownList<br />
  <asp:DropDownList ID="DropDownList1" runat="server">
    <asp:ListItem Item="Item1"</asp:ListItem>
    <asp:ListItem Item="Item2"</asp:ListItem>
    <asp:ListItem Item="Item3"</asp:ListItem>
    <asp:ListItem Item="Item4"</asp:ListItem>
  </asp:DropDownList>
</form>
</body>
</html>
```

Book VI
Chapter 3
Controlling Your
Development
Experience

## 693

## Using multiple-item selection controls
Sometimes you want the user to be able to choose more than one of the items. HTML has two controls that handle that: the listbox and the checkboxlist (See Figure 3-4).

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_693_0.png)

**Figure 3-4:**
Controls for multiple selections.

ASP.NET provides these, like this:

- **The listbox:** This is like a dropdownlist, except there is no expansion — you see the list right away, with scroll bar if needed.
- **The checkboxlist:** This is exactly what it sounds like: a list of boxes. It looks like a radio button list, except with check boxes.

Here is the code for these.

```html
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta runat="server">
<title>MultipleSelection</title>
</head>
<body>
<form id="form1" runat="server">
<div>
  1. The Checkbox List<br />
  <asp:CheckboxList ID="CheckboxList1" runat="server">
    <asp:CheckBoxItem Text="Item 1" Value="1"></asp:CheckBoxItem>
    <asp:CheckBoxItem Text="Item 2" Value="2"></asp:CheckBoxItem>
    <asp:CheckBoxItem Text="Item 3" Value="3"></asp:CheckBoxItem>
    <asp:CheckBoxItem Text="Item 4" Value="4"></asp:CheckBoxItem>
  </asp:CheckboxList>
  <br />
  2. The Listbox<br />
  <asp:ListBox ID="ListBox1" runat="server" Multiple="True">
    <asp:ListItem Item="Item1"</asp:ListItem>
    <asp:ListItem Item="Item2"</asp:ListItem>
    <asp:ListItem Item="Item3"</asp:ListItem>
    <asp:ListItem Item="Item4"</asp:ListItem>
  </asp:ListBox>
  <br />
</div>
</form>
</body>
</html>
```

## 694

## Getting Some Input from the User 669

```html
2. The Listbox<br />
  <asp:ListBox ID="ListBox1" runat="server" Multiple="True">
    <asp:ListItem Item="Item1"</asp:ListItem>
    <asp:ListItem Item="Item2"</asp:ListItem>
    <asp:ListItem Item="Item3"</asp:ListItem>
    <asp:ListItem Item="Item4"</asp:ListItem>
  </asp:ListBox>
</div>
</form>
<body>
</html>
```

## Using other kinds of input controls

ASP.NET provides a number of other input types that are combinations of the above, or are nontitional inputs. (See Figure 3-5) They are all special controls, you need to be in your toolbox so you can use them when the need arises.

- **FileUpload:** The FileUpload does exactly what it says. It creates an HTML input of type **File** and makes the form enctype (encoding type) into multipart form-data. This allows the Web server to accept a long stream of binary data, which you can capture with a streamer.
- **Imagenaps:** Imagemaps are nearly relics of a bygone era. Essentially, they allow you to mark off pixel by pixel maps on top of images and then assign regions within those maps to URLs or other actions.
