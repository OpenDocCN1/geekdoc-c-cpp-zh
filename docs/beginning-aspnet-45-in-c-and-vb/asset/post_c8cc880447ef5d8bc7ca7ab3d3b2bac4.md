
To display a double quote (") in the error message, both languages use a different format. In Visual Basic, you need to double the quotes. In C#, you need to prefix the double quote with a backslash (\) to escape the double quote. In both cases, a double quote character ends up in the error message.

Because every new page you add to the site should now inherit from this new base page, you should create a page template that already has the correct code in its Code Behind and markup, making it easy to add the correct page to the site right from the start. This is discussed next.

## Creating Reusable Page Templates

Visual Studio comes with a great tool to export templates for a number of different file types including ASPX pages, class files, and even CSS files. By creating a custom template, you define the code or markup that you need in every file once and then create new files based on this template, giving you a jump start with the file and minimizing the code you need to type. The next exercise shows you how to create your own templates.

## TRY IT OUT  Creating a Reusable Page Template

In this exercise you see how to create a template file for all new ASPX pages you add to your site. To avoid conflicts with existing pages in your current site, you create a new temporary page and use that for the template. Afterward, you can delete the temporary file.

- 1. Add a new Web Form to the root of the site and call it Temporary.aspx. Make sure it uses Code Behind, uses your programming language, and is based on the master page in the MasterPages folder.
- 2. Open the Code Behind of this new page (by pressing F7) and change the Inherits line (the colon in C#) so the page inherits from BasePage instead of from System.Web.UI.Page. Also rename the class from Temporary to $relurlnamespace$_$safeitemname$:

VB.NET
```vbnet
Partial Class $relurlnamespace$_$safeitemname$
Inherits BasePage
...
End Class
```

C#
```csharp
public partial class $relurlnamespace$_$safeitemname$ : BasePage
{
...
}
```

Make sure you don't remove any of the existing code, like the using statements or the Page_Load method in the C# version.

Don't worry about any compile errors you may get about unexpected characters like $. Once you start adding pages based on this template, $relurlnamespace$_$safeitemname$ will be replaced by the name of the page you're adding.

Type a short note describing the purpose of the template. Make sure the Automatically Import the Template into Visual Studio option is checked. Figure 6-10 shows the final dialog box.

![](img/eadab2ccd79b253c01a3fdff2321202d_272_0.png)

FIGURE 6-10

- 8. Click Finish to create the template. VS opens a File Explorer (Windows Explorer in Windows 7) showing a copy of the new template as a zip file. You can close that window, because you don't need it.

If you want to carry out this exercise for both VB.NET and C#, be sure to rename the resulting zip file first before you make an export for the second language; otherwise the zip file gets overwritten. To rename the file, open File Explorer, go to your Documents folder and then browse to Visual Studio 2012\Templates\ItemTemplates. You'll find a file called MyBasePage.zip, which you can rename to something like MyBasePageCS.zip. Note that the file's location is different from the one you see in Figure 6-10; the output location contains just a copy of the exported template that you can use as a backup.

- 9. Back in VS, delete the temporary file Temporary.aspx you created. Then right-click the website in the Solution Explorer and choose Add New Item. Note that your custom template now shows up in the list of templates, shown in Figure 6-11. If you click it, VS shows you the description you gave it earlier. Note: you may have to restart VS and reopen your website for the template to appear.

- 10. Type a new name for the page, such as `TestPage.aspx`, and click Add to add it to your site. Look at the markup and the Code Behind of the file and verify that `$relurlnamespace$_$safeitemname$ has been renamed to _TestPage to reflect the new name of the page. If everything looks OK, you can delete TestPage.aspx because it's not used in the Planet Wrox website.

![](img/eadab2ccd79b253c01a3fdff2321202d_273_0.png)

FIGURE 6-11

## How It Works

When you export the template, Visual Studio creates a zip file with the necessary files—an ASPX file and a Code Behind file in this exercise. This zip file is then stored in the ItemTemplates subfolder of the Visual Studio 2012 folder under your Documents folder. Some of the files in the zip file contain the placeholders $relurlnamespace$ and $safeitemname$. When you add a new file to the site that is based on your template using the Add New Item dialog box, VS replaces $relurlnamespace$ with the name of the folder (nothing, in the case of a file added to the root of the site) and $safeitemname$ with the actual name of the page. In this exercise, you typed TestPage.aspx as the new name for the page, so you ended up with a class in the Code Behind called _TestPage, which in turn inherits from the global BasePage. The underscore (_) is hard-coded between the two placeholders and is really only needed when adding a Web Form based on this template to a subfolder. However, it's a valid start of a class identifier so you can safely leave it in for pages at the root of your website. If you add a file to a subfolder, such as the Demos folder, the class name is prefixed with the name of the folder so you end up with a class called Demos_TestPage. In addition to $relurlnamespace$ and $safeitemname$, you can use a few other placeholders. Search the MSDN site at http://msdn.microsoft.com for the term $safeitemname$ to find the other template parameters.

If you need to make a change to the exported template, either redo the entire export process, or manually edit the files in the zip file.

Optionally, add one or more skin files to the theme folder. Skins enable you to define individual properties (such as ForeColor and CssClass) for a specific control that are then applied at run time.

After you have followed these steps, you can configure your site or an individual web page to make use of this theme. To be able to set up the correct theme, you should be aware that two types of themes exist.

## Different Types of Themes

An ASP.NET page has two different properties that enable you to set a theme: the Theme property and the StyleSheetTheme property. Both of these properties use the themes that you define in the App_Themes folder. Both of these properties take their default value from the Web.config file as you'll see later. Although at first they seem very similar, it's their runtime behavior that makes the difference. The StyleSheetTheme is applied very early in the page's life cycle, shortly after the page instance has been created. This means that an individual page can override the settings from the theme by applying inline attributes on the controls. So, for example, a theme with a skin file that sets the BackColor of a button to blue can be overridden by the following control declaration in the markup of the page:

```
<asp:Button ID="Button1" runat="server" Text="Button" BackColor="Red" />
```

The theme in the Theme property, on the other hand, is applied late in the page's life cycle, effectively overriding any customization you may have for individual controls.

## Choosing Between Theme and StyleSheetTheme

Because properties of the StyleSheetTheme can be overridden by the page, and the Theme in turn can override these properties again, both serve a distinct purpose. You should set the StyleSheetTheme if you want to supply default settings for your controls. That is, the StyleSheetTheme can supply defaults for your controls, which can then be overridden at the page level. You should use the Theme property instead if you want to enforce the look and feel of your controls. Because the settings from the Theme cannot be overridden anymore and effectively override any customizations, you can be assured that your controls look the way you defined them in the theme. There is one exception: by setting EnableTheming on the control to False you can disable theming for that control. You see this property and its effect toward the end of the chapter. The Planet Wrox sample site in this book uses the Theme property.

## Applying Themes

To apply a theme to your website, you have three different options: at the page level in the Page directive, at the site level by modifying the Web.config file, and programmatically.

Setting the theme at the page level. Setting the Theme or StyleSheetTheme property at the page level is easy, just set the relevant attribute in the Page directive of the page:

```
<%@ Page Language="VB" AutoEventWireup="false" CodeFile="Default.aspx.vb" Inherits="_Default" Theme="DarkGray" %>
```
