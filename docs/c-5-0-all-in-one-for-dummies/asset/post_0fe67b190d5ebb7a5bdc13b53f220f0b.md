
But things get more interesting than that. Say that you want to provide a list of colors and allow the user to select the color of the object in question. You can do that by binding the list of a collection and the selected value to the SelectedItem property of the list control. If you want to show the color itself, you can bind to the FontColor property of a text control.

## Setting up your markup for binding

Back in the Active Server Page days, you put all your data on the page by simply printing it there. Sounds simple, but it had a lot of problems. Foremost, your form had to have a lot of knowledge about the data it was showing. This is a bad thing. Anyway, the format for doing it was

```
<%= ThisIsWhatIWantToPrint %>
```

If you needed a list, you looped in the surrounding code. If you needed a method result, you just put the method right in there. What you saw was what you got.

Data binding is the more enlightened form of getting data on the screen. The controls that are built into ASP.NET know how to handle data on their own, so long as that data meets some basic specifics.

Data binding is accomplished by setting a property of a control to a member of the underlying class. For a single control, like a text box, you just set the property in question, like this:

```
<asp:Label ID="Label1" runat="server" Text="<%# IAmBindingToThisVariable %>" />
```

If you're binding to a repeating control, like a Grid or a ListBox, then you set the DataSource property. I show you how to do that in the next section.

![](img/80ff26f06fc9ab951e1cd4257b867366_715_0.png)

The variables you are binding to need to be in the code-behind and be public. If they aren't, you will get runtime errors. That's also why binding in the code is a good idea, which I do in the next section.

Right now, I'll talk binding in the markup. Here's all you need to do to set up your markup for binding:

- 1. **In the Chapter 3 web project that you've been adding pages with controls to, right-click and choose Add, New Item, and then Class.**
- I named my class Show.
- 2. **Click OK and then put this simple data class in there.**
- This class is just for example — it could be a database or a data class or an Entity Framework model.

```
```csharp
using System;

namespace WebControls
{
    public class Show
    {
        public int ID { get; set; }
        public string ShowTitle { get; set; }
        public String EpisodeTitle { get; set; }
        public DateTime ScheduledTime { get; set; }
        public int Channel { get; set; }
    }
}
```
```

- 3. **Open the Text.aspx file in the Chapter 3 project.**
- 4. **Double-click the design surface to get to the code-behind.**
- If any code already appears in the Page.Load, you can delete it.
- 5. **Add code to the Page.Load to make a mock Show object.**
- In a real project, you would get this object from the database or the service layer. For this example, I just use mock code:

```
```csharp
Show show = new Show { ID = 1, Channel = 5,
    EpisodeTitle = "ASP.NET Databinding", ScheduledTime
    = new DateTime(2009, 4, 12, 12, 0, 0), ShowTitle =
    "The C# Show" };
```
```

- 6. **Tell the page that you’re going to be data binding by adding a** `Page.DataBind()` **call at the end of the Page_Load.**
- The finished method looks like this:

```
```csharp
protected void Page_Load(object sender, EventArgs e)
{
    Show show = new Show { ID = 1, Channel = 5, EpisodeTitle = "ASP.NET
    Databinding", ScheduledTime = new DateTime(2009, 4, 12, 12, 0, 0),
    ShowTitle = "The C# Show" };
    Page.DataBind();
}
```
```

- 7. **Change to the markup in the designer.**
- The Text field gets the markup for the binding.
- 8. **You can just give text field the property, like this:**

```
```aspx
<asp:Label ID="Label1" runat="server" Text='<%# show.EpisodeTitle %>'></asp:Label>
```
```

This isn’t the interesting way to bind things. It is nice because you can edit the binding without recompiling, but the interesting way is in the C# code. Doing it in the C# code is much more readable and manageable. There are times to use each, but this is a C# book. The least I can do is to focus on the code-behind, right?

![](img/80ff26f06fc9ab951e1cd4257b867366_716_0.png)

## Data binding using the code-behind

Rather than set a property directly in the markup, you can set it equal to a value in the code-behind. For a repeating control, you can set a DataSource property in the C# code for the control. Then, when you bind the page, it uses that value to load in the right value or values from the code-behind.

Keep in mind, though, that with the Text property of a Label (for instance) this is just simple data binding. I am just setting a value.

Try it with the Show example. Just follow these steps:

1. Keep the label text simple — just drop the Text property, like this:

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Text.aspx.cs" Inherits="Chapter_3_Text" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" >
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>

    This is some text.<br />
    <asp:Label ID="Label1" runat="server" />

</div>
</form>
</body>
</html>
```

2. In the code-behind, set the Text property equal to the property on the control that you want to bind to.

Notice that there is no DataBind command for the page:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace Chapter_3
{
    public partial class Text : System.Web.UI.Page
    {
        public Show show;
        protected void Page_Load(object sender, EventArgs e)
        {
            show = new Show { ID = 1, Channel = 5, EpisodeTitle = "ASP.NET Databinding", ScheduledTime = new DateTime(2009, 4, 12, 0, 0), ShowTitle = "The C# Show" };
```

```
Label1.Text = show.EpisodeTitle;
}
}
```

- 3. Run the application to see the value get set.

This works well, but remember, this is only simple data binding. It's just setting values. Full data binding is for controls with repeating properties.

## Using commonly bound controls

After all this label stuff, I talk about what data binding is really good for — collections. Data binding is great for dealing with groups of items, bound to repeating structures in HTML.

The typical example of data binding is the DataGrid control. If everything is set up correctly, you have remarkable control over how the grid looks. If things aren't named correctly, you still have the option to show all of the data in a default style. To create a databound grid, follow these steps:

- 1. Add a new ASPX file to the projects called Grid.aspx.
- 2. Change to design view.
- 3. Open the Data section of the Toolbox and drag a GridView onto the design surface.
- 4. Double-click the design surface to change to Code View and get a page load event handler.
- 5. Make a mock collection of Shows in the page load event handler.

I used a generic list of Show.

```
List<Show> shows = new List<Show>();
protected void Page_Load(object sender, EventArgs e)
{
    shows.Add(new Show { ID = 1, Channel = 5, EpisodeTitle = "ASP.NET Databinding", ScheduledTime = new DateTime(2009, 4, 12, 12, 0, 0), ShowTitle = "The C# Show" });
    shows.Add(new Show { ID = 2, Channel = 5, EpisodeTitle = "ASP.NET Styling", ScheduledTime = new DateTime(2009, 4, 12, 13, 0, 0), ShowTitle = "The C# Show" });
    shows.Add(new Show { ID = 3, Channel = 8, EpisodeTitle = "Inheritance", ScheduledTime = new DateTime(2009, 4, 16, 9, 0, 0), ShowTitle = "Learning C#" });
    shows.Add(new Show { ID = 4, Channel = 8, EpisodeTitle = "Partial Classes", ScheduledTime = new DateTime(2009, 4, 17, 9, 0, 0), ShowTitle = "Learning C#" });
    shows.Add(new Show { ID = 5, Channel = 8, EpisodeTitle = "Operator Overloading", ScheduledTime = new DateTime(2009, 4, 18, 9, 0, 0), ShowTitle = "Learning C#" });
}
```
