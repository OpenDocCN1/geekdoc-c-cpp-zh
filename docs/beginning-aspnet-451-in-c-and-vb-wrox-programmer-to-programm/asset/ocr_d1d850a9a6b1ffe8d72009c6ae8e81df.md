# Introduction to User Controls | 27

8. Using the same Properties Grid, locate the AlternateText property and type This is a sample banner. Most browsers display the alternate text (rendered as a client-side alt attribute) when the image cannot be displayed. Some older browsers show the alternate text as the tooltip for when you hover your mouse over it.

9. Wrap the Image in a standard <a> element and set its href attribute to http://pzp.wrox.com. If you want to, you can use a code snippet to insert a link for the you. To do this, type the letter and then press Tab. Vs inserts a link and enables you to type in the href value directly. When you press Tab again, the content of the link is selected, you can delete by pressing Del (the Image will be the contents of the link). Finally, close the </a> tag and move it after the image.

10. Set the target of the anchor <a> to blank to force the browser to open the page in a new window when the image is clicked. When you're, the code for the user control should look like the following code, for the Language attribute that you may have to VB and the AutoEventWire is False in VB.NET.

```
<@ Language="C#" AutoEventWire="true" CodeFile="Banner.asc.cs"
<asp:Panel ID="Vertical" run="server">
  <a href="http://pzp.wrox.com" target="blank">
  <asp:Image ID="Image" run="server" AlternateText="This is a sample banner"
  ImageUrl="/Images/Banner120x240.gif" />
  </a>
</asp:Panel>
```

11. Save the changes by pressing Ctrl+S and close the user control by pressing Ctrl+F4.

# How It Works

The design experience of user controls in the Visual Studio IDE is identical to that of pages. You can use and drop; the Toolbox; the Markup, Split, and Design Views; and so on. This makes it easy to work with user controls because you can use all the familiar tools you use for development.

The control you just created displays a single image wrapped in an anchor element. In the next section, you will see how to add the control to the master page so it will be displayed in the Sidebar element of every page in the site. Later sections in this chapter show you how to add the other image that you can use to display a horizontal banner in individual pages.

# Adding User Controls to a Content Page or Master Page

To use a user control in a master page or in another user control, you need to perform two steps. First, you must register the control by adding an @ Register directive to the page or control where you want the user control to appear. The second step involves adding the tags for the user control to the page and optionally setting some attributes on it.

A typical @ Register for a user control looks like this:

```
<@ Src="ControlName.ascx" TagName="ControlName" TagPrefix="ucl" %>
```