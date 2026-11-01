
4. Make sure you're in Markup View, and directly under the opening Content tag and before the GridView add the following markup that creates a table with one row and two cells, each with a large heading (h1) and a Label control called NoPostBack and PostBack, respectively.

```html
<table>
<tr>
<td><h1>No PostBack</h1><asp:Label ID="NoPostBack" runat="server" /></td>
<td><h1>PostBack</h1><asp:Label ID="PostBack" runat="server" /></td>
</tr>
</table>
```

5. Switch to Design View, and below the GridView drop a Button control and double-click it in Design View to set up an event handler for its Click event in the Code Behind.

6. Switch back to Design View and double-click the gray and read-only area of the page to set up a handler for the Page control's Load event.

7. Switch to Design View again, click the GridView, and open its Properties Grid by pressing F4. Switch to the Events tab and double-click the following events to set up handlers for them in the Code Behind. After each handler, switch back to Design View by pressing Ctrl+Tab so you can add the next event.

   - Sorted
   - Sorting
   - RowCreated
   - DataBinding
   - DataBound
   - RowDataBound

8. Repeat the preceding step, but now set up the following events for the EntityDataSource control:

   - ContextCreating
   - Selecting

9. Make sure you are in Code Behind and at the top of the file add the following Imports/using statement:

### VB.NET

```vbnet
Imports System.Runtime.CompilerServices
```

### C#

```csharp
using System.Runtime.CompilerServices;
```

Then below the last event handler (but still within the class definition), add the following method that writes some text to one of the two labels, depending on whether the current page request is the result of a postback:

### VB.NET

```vbnet
Private Sub WriteMessage(<CallerMemberName> Optional handlerName As String = "")
    If Page.IsPostBack Then
        PostBack.Text &= handlerName & "<br />"
    Else
        NoPostBack.Text &= handlerName & "<br />"
    End If
End Sub
```

### C#

```csharp
private void WriteMessage([CallerMemberName] string handlerName = "")
{
    if (Page.IsPostBack)
    {
        PostBack.Text += handlerName + "<br />";
    }
    else
    {
        NoPostBack.Text += handlerName + "<br />";
    }
}
```

10. To each of the event handlers that you have set up, add the following code that calls your custom method. Because you're not passing a value for the optional handlerName parameter, .NET automatically inserts the name of the calling method because of the CallerMemberName attribute applied to that parameter in the WriteMessage method. You see how this works later.

### VB.NET

```vbnet
Private Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    WriteMessage()
End Sub
```

### C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    WriteMessage();
}
```

11. Finally, add the following event handler to the Code Behind manually:

### VB.NET

```vbnet
Protected Sub Page_PreRenderComplete(sender As Object, e As EventArgs) Handles Me.PreRenderComplete
    WriteMessage("Page_PreRenderComplete<br />------")
End Sub
```

### C#

```csharp
protected void Page_PreRenderComplete(object sender, EventArgs e)
{
    WriteMessage("Page_PreRenderComplete<br />------");
}
```

The PreRenderComplete event fires very late in the Page control's life cycle, making it an ideal place to put a line at the bottom of the event list. That way you can clearly see what set of events belong to each other, which in turn helps you to figure out what events are triggered during page load or a postback.

12. Save all your changes and open the page in the browser. In addition to the GridView with the available genres, you should also see a list with event names under the No PostBack heading:

```
Page_Load
EntityDataSource1_ContextCreating
EntityDataSource1_Selecting
GridView1_DataBinding
GridView1_RowCreated
GridView1_RowDataBound
GridView1_RowCreated
GridView1_RowDataBound
...
GridView1_DataBound
Page_PreRenderComplete
----------
```

Note that the RowCreated and RowDataBound events are repeated multiple times — once for each genre from the database plus two more. You see later why that is. Click the button below the GridView to cause a postback. The No PostBack label won't change, but the PostBack label now shows the following list of event names:

```
GridView1_RowCreated
GridView1_RowCreated

GridView1_RowCreated
GridView1_RowCreated
Page_Load
Button1_Click
Page_PreRenderComplete
----------
```

Click one of the column headers of the GridView to order the data it is displaying. Notice that the second label's text is extended with a second set of event names. Each set is separated by a line of dashes, created by the Page_PreRenderComplete event handler.

## How It Works

Technically, this exercise isn't complicated. You set up a bunch of event handlers for the various controls in your page. Inside the event handler you call a method that checks whether the page is currently loading for the first time or is loading due to a postback. To make it easy to add the name of the calling method to the Label control, the handlerName parameter of the method has a special CallerMemberName attribute applied, like this:

### VB.NET

```vbnet
Private Sub WriteMessage(<CallerMemberName> Optional handlerName As String = "")
```

### C#

```csharp
private void WriteMessage([CallerMemberName] string handlerName = "")
```

This attribute is new in .NET 4.5 and can be applied to optional parameters (identified in VB.NET with the Optional keyword and a default value, and in C# simply by assigning it a default value). When no value is passed to the WriteMessage method for this parameter (as is the case for most of the handlers except for the last one you added), .NET fills it for you with the name of the calling method. This is very convenient for debugging purposes because it enables you to easily figure out which method called WriteMessage. In previous versions of .NET you had to pass the name of the calling method manually in each call to WriteMessage, making this code a bit more tedious to write. Also, because this attribute only has an effect when no value is passed in, you can still supply a value yourself, as is the case with the Page_PreRenderComplete handler. Besides the method name, this code also passes the line break and the dashed line and, as such, you have to supply the value yourself.

The WriteMessage method then updates one of the two Label controls with the name of the event that triggered the event handler.

What's also interesting about this exercise is the order in which the events occur. Take a look at the first list, displayed when the page first loads:

```
Page_Load
EntityDataSource1_ContextCreating
EntityDataSource1_Selecting
GridView1_DataBinding
GridView1_RowCreated
GridView1_RowDataBound
GridView1_RowCreated
GridView1_RowDataBound
...
GridView1_DataBound
Page_PreRenderComplete
------------------
```

First Page_Load is triggered. Then the GridView sees that it's hooked up to an EntityDataSource and asks that control for its data. This causes the ContextCreating and Selecting events to be triggered. When the GridView receives the data from the EntityDataSource, it fires its DataBinding event to signal it's about to bind the data to the control. The GridView then starts to create its rows. For each item in the data source, it creates a row, fires RowCreated, binds the item's data to the row, and finally calls RowDataBound. If you carefully count the number of times that RowCreated and RowDataBound are called, you'll notice that the total number of calls is the actual number of items that are in the data source plus two. This is because the same event is also raised when the control creates its header and footer rows. You see how to distinguish between these rows inside an event handler in a later exercise.

Finally, when the GridView is done creating and binding all the rows in the data source, it fires its DataBound event.

On postback, the story looks quite different. When you click the button to cause a postback, the following events are raised:

```
...
GridView1_RowCreated
GridView1_RowCreated
GridView1_RowCreated
GridView1_RowCreated
Page_Load
```
