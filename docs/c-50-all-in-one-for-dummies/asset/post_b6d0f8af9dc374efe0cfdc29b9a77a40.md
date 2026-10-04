
# Showing Stuff to the User 679

![](img/6df7bb88e9302e98442acc219cfbd7fc_704_0.png)

**Figure 3-1:**
There is text, and there is:

Book VI
Chapter 3
Experience Development
Controlling Your

## ## 7. Change the value of the label in the Page.Load event handler by setting the Text property.

The new handler should look like this:

```assembly
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.Controls;

namespace WebControls
{
    public partial class Text : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            Label1.Text = "This is some text from the codebehind";
        }
    }
}
```

## ## 8. Press <F5> to launch the application.

You'll see the label text was set by the C# code.

How to decide between labels and text? It's usually easy. Use a label if the text will need to change based on input from the user or the server. Use text if the text is static. A description of an item that is loaded from a database? That's a label. Your CEO's bio? That's text.

# Showing Stuff to the User

# Images

Images are next to text in the realm of standard website fare. It's a complex topic because few programmers are graphic artists, and making nice images that fit together and look good is hard.

Nonetheless, sometimes you just want to show a picture on a page. Just as with text, there are two ways you can go about this. (Okay, there are more than two.) You can use the HTML `<img>` tag, or you can use the ASP.NET Image control.

Differences? Same as the text: If you need an image that you can manage from the C# side of things, use an image control — a product image, for example. If it is just a static image, like the picture of your CEO, then you can use the HTML tag.

Just follow these steps to add an image with ASP.Net's Image control:

- 1. Add two images to your project by right-clicking the project and choosing Add:Existing Item. You can find images or download some. I used a drum and a tuba. (It's college football time!)
- 2. Add a new page called Images.aspx.
- 3. Drag one of the pictures right into the box that denotes the div. You'll get the Accessibility Properties dialog box, and then the picture will just right up.
- 4. Press Enter a few times to make some space.
- 5. Drag an image control from the Toolbox to the page where the cursor is sitting. It should appear as a broken image. That's okay.
- 6. Double-click elsewhere on the page to get the Page.Load event handler and switch to Code View.
- 7. Just like I did in the Text example, set the visible property of the control. In this case, it is ImageUrl. The new code should look like this:

```assembly
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace WebControls
{
    public partial class Images : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            Image.ImageUrl = "tuba.gif";
        }
    }
}
```

- 8. Right-click the Images.aspx page in the Solution Explorer and select Set As Start from the context menu.
- 9. Press <F5> to see it run.

You're probably getting the idea by this point. You can use HTML and set static values, or you can use the ASP.NET controls and set dynamic values. In the examples here, you're obviously just "static" dynamic values, but you could be reading from a web service, a database, or even calculating the values. Images can be listed from a directory. Text could be generated and read into a table. The options are endless.

# Panels and multiews

Managing all these text blocks and images can be rough. ASP.NET provides a number of tools to help, including the two following:

- Panels are just divs you can manage in code-behind. Just like the text and images you added in the preceding section, panels can be named and controlled in C#. The server will process changes before it sends the HTML to the browser. This helps to break the content into manageable groups.
- Multiews are essentially containers that hold a lot of panels. You can use them for wizards and tag groupings. They help to manage the panels, which help manage the content. For more information, MSDN for ASP.NET.

From the client's perspective, panels and multiews are effectively the same structure, but they provide developers with a few options. For instance, the multiew shows only one view of itself by default, whereas you have to hide panels that are not in use.

# Tables

Tables work like other web controls. In HTML, you have the basic `<table>`, `<tr>`, and `<td>` tags. In ASP.NET, there is a Table control, with TableRows and TableCells. If you add an ASP.NET table, it looks like this:

# 682 Getting Input from the User

```asp
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Tables.aspx.cs" Inherits="Chapter_3.Tables" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN" "http://www.w3.org/TR/html/xhtml-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>runat="server"</title>
</head>
<body>
<form id="form1" runat="server">
<asp:Table Id="Table1" runat="server">
<asp:TableRow runat="server">
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
</asp:TableRow>
<asp:TableRow runat="server">
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
</asp:TableRow>
<asp:TableRow runat="server">
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
</asp:TableRow>
<asp:TableRow runat="server">
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
</asp:TableRow>
<asp:TableRow runat="server">
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
</asp:TableRow>
</asp:Table>
</form>
</body>
</html>
```

So what's the process of creating tables this way? Well, you can name rows and cells and then manage them in C#. In all honesty, that's not I recommend doing things. Tables are good for two things — layout and tabular data. Layout has been superseded by CSS.

For tabular data, tables still work. However, there is a more interesting solution. The GridView (found in the Data section) is just as functional — and it is bindable. I chat more about that in the “Data Binding” section, later in this chapter.

# Getting Input from the User

Acquiring input from the user is one of the most significant processes that web developers do. Data-active web is all interactivity; Web 2.0 is all about interactivity. Getting information from a user is a job one.

# Getting Input from the User 683

You can do a lot of things to get input from the user, but there is a subset of the controls that are generally considered to be user input. You'll use those controls a lot.

# Using input controls

The most obvious form of collecting data from a user is the text input boxes, as shown in Figure 3-2. In HTML, there are three defined controls: the textbox, the password, and the textarea. The TextBox ASP.NET control handles all of these. A TextMode tells how to render the control.

To use the TextBox control, drag it into the designer from the Toolbox. You can change the property of a control instance — the only other significant element — in the ASP.NET markup, the property panel, or the C# code.

The properties that you are the most interested in include

- **ID**: The name that you use to reference the control in the C# code. This needs to be set first, before you can use the control.
- **TextMode**: This determines the type of text box that gets rendered.
- **MaxLength**: The maximum number of characters that the user can use in the field. Note that this doesn't work when the TextMode is defined as TextArea.
- **Height and Width**: The size that the text box appears on the page.
- **Css**: The style sheet class that the control will be rendered to use. Must be used in conjunction with a style sheet.
