4. Make sure you're in Markup View, and directly under the opening Content tag and before the GridView add the following markup that creates a table with one row and two cells, each with a large heading (h1) and a Label control called NoPostBack and PostBack, respectively.

```
```html
<table>
<tr>
<td><h1>No PostBack</h1><asp:Label ID="NoPostBack" runat="server" /></td>
<td><h1>PostBack</h1><asp:Label ID="PostBack" runat="server" /></td>
</tr>
</table>
```
```

5. Switch to Design View, and below the GridView drop a Button control and double-click it in Design View to set up an event handler for its Click event in the Code Behind.

6. Switch back to Design View and double-click the gray and read-only area of the page to set up a handler for the Page control's Load event.

7. Switch to Design View again, click the GridView, and open its Properties Grid by pressing F4. Switch to the Events tab and double-click the following events to set up handlers for them in the Code Behind. After each handler, switch back to Design View by pressing Ctrl+Tab so you can add the next event.

+   - Sorted
+   - Sorting
+   - RowCreated
+   - DataBinding
+   - DataBound
+   - RowDataBound

8. Repeat the preceding step, but now set up the following events for the EntityDataSource control:

+   - ContextCreating
+   - Selecting

9. Make sure you are in Code Behind and at the top of the file add the following Imports/using statement:

```
```vbnet
VB.NET
Imports System.Runtime.CompilerServices
```
```csharp
C#
using System.Runtime.CompilerServices;
```
```

Then below the last event handler (but still within the class definition), add the following method that writes some text to one of the two labels, depending on whether the current page request is the result of a postback: