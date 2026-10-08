The big benefit to MVC over other kinds of Web apps is that the user interface code is much more testable with automated tests. In fact, when you start an ASP.NET MVC project, it asks you to create a test project along with it.

Another difference from n-tier is some formalization to the implementation of MVC. It is a project type, and rather than having to figure out how things hook up, MVC does some of the work for you.

MVC is a big topic that I just can't cover here in any detail. If you have a large project for which you need to divide up the work among developers with varying skill sets, it's cool. Read more in Professional ASP.NET by Wrox Press.

## Chapter 3: Controlling Your Development Experience

## In This Chapter

- Showing stuff to the user
- Getting some input from the user
- Binding
- Styling with the best
- Making sure the site is accessible
- Constructing user controls
- Adding custom controls

ASP.NET is a rendering engine. It takes preset batches of functionality and renders it into HTML. For instance, ASP.NET can take a database table and render a little bit of layout information and make a nice, dynamic HTML table.

Rendering engines are a good idea in the W World. With a bunch of different implementations and versions, your rendering engine can produce different user markup out of the same effective code base.

ASP.NET does not do this well. You can tell it to make mobile-device markup and text-only markup and Internet Explorer markup from the same ASP.NET file, and it will do an okay job.

This is possible because of Web controls. Web controls are controls that ASP.NET renders into client-side markup, like HTML, CSS, and JavaScript. Well-programmed controls protect the developer from the implementation details but still do what needs to be done when the times come.

Web controls aren't anything special. Basically, they show a pretty text box in the designer pane of Visual Studio, and then emit text an `<input>` tag — when called upon to do so.

ASP.NET has a lot of included controls, many controls are available from third-party providers, and you can even build your own and base them on existing controls. It's a good system.

## Showing Stuff to the User

Web surfers want to look at stuff. For them to look at it, you have to show it. Most of the controls in the ASP.NET control library are about showing things to the user.

Although there are a lot of controls, some of them apply to the subject matter of this book — C#. This doesn't mean you shouldn't use them, but they are more about the HTML and less about the code on the server. So I am just going to cover a few controls. For more, pick up ASP.NET For Dummies.

### Labels versus plain text

The basic item on an average Web page is text. Take a look at a normal site, like Microsoft.com. You find a text box, maybe two; a handful of images also. Most of what there is text.

Text comes in a few flavors in ASP.NET. The two I want to talk about are Label text and, plain text. Label text is text inside a named span that you can change with C# code. Then there is just text on the page. This text is static — downloaded to the client just as you typed it.

To see what I mean, start a new Web project. Follow these steps:

1. Click the New Project button and select C# ASP.NET project.

2. Make a new ASP.NET page called Text.aspx.

3. Change to Design view.

There will be a default div that you saw in Chapter 2. Put your cursor between the `<div>` and the `</div>` and then type something innovative, like "This is new text." Then press Enter.

4. On the new line, drag a Label from the Toolbox.

Your finished product should look like Figure 3-1.

5. Double-click the value of the label in the Page.Load event handler to get the code-behind.

6. Change the value of the label in the Page. The new handler should look like this:

```sharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
```

```sharp
namespace Chapter_3
{
    public partial class Text : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            Label.Text = "This is some text from the codebehind.";
        }
    }
}
```

7. Press <F5> to launch the application.

You'll see that label text by the C# code.

How to decide between labels and text? It's usually easy. Use a label if the text will need to change based on input from the user or use text if the text is static. A description of an item that is loaded from a database? That's a label. Your CEO's bio? That's text.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_686_0.png)

Figure 3-1:
There is text, and there is text.

## Images

Images are next to text in the realm of standard Web site fare. It's a popular topic because programmers are graphic artists, and making nice images that fit together look good is hard.

Nonetheless, sometimes you just want to show a picture on a page. Just as with text, there are two ways you can do this. (Okay, there are more than two.) You can use the HTML `<img>` tag, or you can use the ASP.NET Image control.

Differences? Same as the text: If you need an image that you can manage from the C# side of things, use an image control: a product image, for example. If it is a static image, like the picture of your CEO, then use the HTML tag.

Just follow these steps to add an image with ASP.NET's Image control:

1. Add two images to your project by right-clicking the project and choosing Add: Existing Item.

You can find two images, or download some. I used a drum and a tuba. (It's college football!)

2. Add a new page called Images.aspx.

3. Drag one of the pictures right into the box that denotes `div`.

You'll get the Accessibility Properties dialog box, and then the picture will just show right up. Press Enter a few times to make some space.

4. Drag an image control from the Toolbox onto the page where the cursor is sitting. It should appear as a broken image. That's okay.

5. Double-click elsewhere to get the Page.Load event handler and switch to Code View.

6. Just like we did in the Text example, the visible property of the control. In this case, it is ImageUrl. The new code should look like this:

```sharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.Controls;

namespace Chapter_3
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

7. Right-click the Images.aspx page in the Solution Explorer and select Set as Start Page from the context menu.

8. Press <F5> to see it run.

You are probably getting that label text by the C# code.

## Showing Stuff to the User

Web surfers want to look at stuff. For them to look at it, you have to show it. Most of the controls in the ASP.NET control library are about showing things to the user.

Although there are a lot of controls, some of them apply to the subject matter of this book — C#. This doesn't mean you shouldn't use them, but they are more about the HTML and less about the code on the server. So I am just going to cover a few controls. For more, pick up ASP.NET For Dummies.

### Panels and Multiews

Panels are just divs. From the client's perspective, panels and multiviews are effectively the same. The multiview shows only one view of itself by default, where you have to hide panels that are not used.

Multiews are controls that hold a lot of panels. You can use them.

### Tables

Tables work like other controls. In ASP.NET, you have the `<table>`, `<tr>`, and `<td>` tags. In ASP.NET there is a Table control, with TableRows and TableCells. If you add an ASP.NET table, it could look like this:

```html
@@ Language="C#" CodeBeh="Tables.aspx.cs"
Inherits="Tables.Tables">

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML1.0 Transitional//EN" "http://www.w3.org/TR/html1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta runat="server">
<title>title</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Table Id="Table" runat="server">
<asp:TableRow runat="server">
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
</asp:TableRow>
<asp:TableRow runat="server">
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
</asp:TableRow>
<asp:TableRow runat="server">
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
</asp:TableRow>
</asp:Table>
</div>
</form>
</body>
</html>
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_688_0.png)
