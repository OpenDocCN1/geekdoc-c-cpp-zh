Properties Grid. This enables you to delete reviews from the database using the GridView later. The Fields dialog box should now look like Figure 13-13.

![](bbox=[0.12, 0.2, 0.78, 0.62])

FIGURE 13-13

+   6. Click the Authorized column in the Selected Fields list and then click the blue Convert This Field into a TemplateField link visible at the bottom-right of the dialog box in Figure 13-13.
+   7. Click the CreateDateTime column on the left and set its DataFormatString property to {0:g}.
+   8. Click OK to apply the changes to the source code.
+   9. Switch to Markup View and remove the <EditItemTemplate> for the Authorized field. The GridView displays reviews only in read-only mode, so you don't need this template.
+   10. Modify the Label control in the ItemTemplate of the Authorized field so it ends up like this:
+   <asp:Label ID="AuthorizedLabel" runat="server" Text='<%# GetBooleanText(Eval("Authorized")) %>' />
+   11. Switch to the Code Behind of the page by pressing F7 and add the following function—which returns the text Yes or No depending on the boolean value that you pass—to the top of the class file, right after the Inherits line in VB.NET and after the opening curly brace in C#.

# VB.NET

```
Inherits System.Web.UI.Page
Protected Function GetBooleanText(booleanValue As Object) As String
    Dim authorized As Boolean = CType(booleanValue, Boolean)
    If authorized Then
        Return "Yes"
```