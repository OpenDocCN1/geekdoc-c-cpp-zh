+   9. Change the (ID) to TextToChange.
+   10. Click the Button in the designer.
+   11. Change the Text property to Click Me.
+   12. Change the (ID) to ChangeText.

The Properties panel changes to show the button's properties.

Now change back to Source view and note the changes in the code:

```
<%@ Page Language="VB" AutoEventWireup="false" CodeFile="Default.aspx.cs" Inherits="AspNetFirstSample._Default" %>

<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="AspNetFirstSample._Default" %>

<asp:Content runat="server" ID="FeaturedContent" ContentPlaceHolderID="FeaturedContent">
<section class="featured">
<div class="content-wrapper">
<hgroup class="title">
<h1>Title 1</h1>
<h2>Modify this template to jump-start your ASP.NET application.</h2>
</hgroup>
</div>
<p>
To learn more about ASP.NET, visit <a href="http://asp.net" title="ASP.NET Website">http://asp.net</a>.
The page features <mark>videos, tutorials, and samples</mark> to help you get the most from ASP.NET.
If you have any questions about ASP.NET visit forums</a> <a href="http://forums.asp.net/18.aspx" title="ASP.NET Forum">our forums</a>.
</p>
</div>
</section>
<asp:Content runat="server" ID="BodyContent" ContentPlaceHolderID="MainContent">
<asp:Label ID="TextToChange" runat="server" Text="This is the text to change" Font-Size="14pt"></asp:Label><br /><br />
<asp:Button ID="ChangeText" runat="server" Text="Click Me" />
</asp:Content>
```

So the management of your code is what the designer does for you. Now, some people don't like Visual Studio messing with their code. Some people don't like to remember all the ins and outs of ASP.NET. It's all up to you; you can use it or not.

This isn't where the magic is, though. This is a C# book, and if you're working in a big shop, your ASP.NET code is probably being written for you anyway. You want to play with the server code, and I don't blame you.