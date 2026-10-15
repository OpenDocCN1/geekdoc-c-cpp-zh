use some built-in capabilities from Visual Studio to convert the page to a format that enables you to plug in other languages easily.

To see this in action, build a simple ASP.NET website called ProVB_Localization and open the Default.aspx page as presented here. Note that we have added a few simple controls to replace the default labels generated with a new page. This page will be referred to later in the chapter as the “ASP.NET page code block.” Keep in mind that the downloaded code will not match this initial code snippet as this chapter modifies this code to support multiple languages.

```
<%@ Page Title="Home Page" Language="VB" MasterPageFile="~/Site.Master" AutoEventWireup="false" CodeFile="Default.aspx.vb" Inherits="_Default" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">

<div>
<asp:Label ID="Label1" runat="server"
Text="What is your name?"></asp:Label><br />
<br />
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>&nbsp;
<asp:Button ID="Button1" runat="server" Text="Submit Name" /><br />
<br />
<asp:Label ID="Label2" runat="server"></asp:Label>
</div>

</asp:Content>
```

Code snippet from ProVB_Localization\Default.aspx

As you can see, there is not much to this page. It is composed of a couple of Label controls, as well as TextBox and Button controls. Update the click event handler for Button1 to set the Label2.Text property text to the TextBox1.Text property value. This way, when users enter their name into the text box, the Label2 server control is populated with the inputted name.

The next step is what makes Visual Studio so great. To change the construction of this page so that it can be localized easily from resource files, open the page in Visual Studio and ensure that you are in Design view. Next, using the Visual Studio menu, select Tools ➔ Generate Local Resource. Note that you can select this tool only when you are in the Design view of your page.

Selecting Generate Local Resource from the Tools menu causes Visual Studio to create an App_LocalResources folder in your project if you don’t have one already. A .resx file based upon this ASP.NET page is then placed in the folder. For instance, if you are working with the Default.aspx page, then the resource file is named Default.aspx.resx (see Figure 27-11).

Right-click on the .resx file, select View Code. If View Code isn’t present on your default menu, select Open With; you’ll get a dialog with a list of editor options. From the Open With dialog, select the XML (Text) Editor as the program to open this file using the OK button. After doing this, you should find the View Code option on the context menu for this file. When the .resx file opens, you’ll notice that the .resx file is nothing more than an XML file with an associated schema at the beginning of the document. The resource file that is generated for you takes every possible property of every translatable control on the page and gives each item a key value that can be referenced in your ASP.NET page. Looking at the page’s code, note that all the text values you placed in the page have been retained, but

![](bbox=[0.72, 0.46, 0.9, 0.71])

FIGURE 27-11