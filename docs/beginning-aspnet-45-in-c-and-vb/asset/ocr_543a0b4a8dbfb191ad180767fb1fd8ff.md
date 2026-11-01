To display a double quote (") in the error message, both languages use a different format. In Visual Basic, you need to double the quotes. In C#, you need to prefix the double quote with a backslash (\) to escape the double quote. In both cases, a double quote character ends up in the error message.

Because every new page you add to the site should now inherit from this new base page, you should create a page template that already has the correct code in its Code Behind and markup, making it easy to add the correct page to the site right from the start. This is discussed next.

# Creating Reusable Page Templates

Visual Studio comes with a great tool to export templates for a number of different file types including ASPX pages, class files, and even CSS files. By creating a custom template, you define the code or markup that you need in every file once and then create new files based on this template, giving you a jump start with the file and minimizing the code you need to type. The next exercise shows you how to create your own templates.

# TRY IT OUT  Creating a Reusable Page Template

In this exercise you see how to create a template file for all new ASPX pages you add to your site. To avoid conflicts with existing pages in your current site, you create a new temporary page and use that for the template. Afterward, you can delete the temporary file.

+   1. Add a new Web Form to the root of the site and call it Temporary.aspx. Make sure it uses Code Behind, uses your programming language, and is based on the master page in the MasterPages folder.
+   2. Open the Code Behind of this new page (by pressing F7) and change the Inherits line (the colon in C#) so the page inherits from BasePage instead of from System.Web.UI.Page. Also rename the class from Temporary to $relurlnamespace$_$safeitemname$:

```
VB.NET
```vbnet
Partial Class $relurlnamespace$_$safeitemname$
Inherits BasePage
...
End Class
```
```

```
C#
```csharp
public partial class $relurlnamespace$_$safeitemname$ : BasePage
{
...
}
```
```

Make sure you don't remove any of the existing code, like the using statements or the Page_Load method in the C# version.

Don't worry about any compile errors you may get about unexpected characters like $. Once you start adding pages based on this template, $relurlnamespace$_$safeitemname$ will be replaced by the name of the page you're adding.