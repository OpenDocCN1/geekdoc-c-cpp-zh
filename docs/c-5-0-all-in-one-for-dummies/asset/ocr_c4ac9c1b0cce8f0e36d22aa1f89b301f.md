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

+   3. **Open the Text.aspx file in the Chapter 3 project.**

+   4. **Double-click the design surface to get to the code-behind.**
+   
+   If any code already appears in the Page.Load, you can delete it.

+   5. **Add code to the Page.Load to make a mock Show object.**
+   
+   In a real project, you would get this object from the database or the service layer. For this example, I just use mock code:

```
```csharp
Show show = new Show { ID = 1, Channel = 5,
    EpisodeTitle = "ASP.NET Databinding", ScheduledTime
    = new DateTime(2009, 4, 12, 12, 0, 0), ShowTitle =
    "The C# Show" };
```
```

+   6. **Tell the page that you’re going to be data binding by adding a** `Page.DataBind()` **call at the end of the Page_Load.**
+   
+   The finished method looks like this:

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

+   7. **Change to the markup in the designer.**
+   
+   The Text field gets the markup for the binding.

+   8. **You can just give text field the property, like this:**

```
```aspx
<asp:Label ID="Label1" runat="server" Text='<%# show.EpisodeTitle %>'></asp:Label>
```
```

This isn’t the interesting way to bind things. It is nice because you can edit the binding without recompiling, but the interesting way is in the C# code. Doing it in the C# code is much more readable and manageable. There are times to use each, but this is a C# book. The least I can do is to focus on the code-behind, right?

![](bbox=[0.882, 0.324, 0.997, 0.49])