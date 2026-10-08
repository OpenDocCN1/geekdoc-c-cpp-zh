# 644 Working in Visual Studio

Change to the Source view, where you started. Check out the designer
source we'll break down the ASP.NET code from the HTML code a bit.
Here is the code for the controls are added:

```
<@ Page Language="C#" AutoEventWireup="true" CodeBehind="Default.aspx"
Inherits="ASPNetFirst_Example.Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN" "http://www.
w3.org/TR/html-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>title</title>
</head>
<body>
<form id="form" runat="server">
<div>
<asp:Label ID="Label" runat="server" Text="Label"></asp:Label>
</div>
<p>
<asp:Button ID="Button1" runat="server" Text="Button" />
</p>
</form>
</body>
</html>
```

If you have experience with HTML, you recognize 90 percent of what is
the screen. <html>, <head>, <body>, and <form> are all common HTML
tags that you can find on any Web page. The two tags that you begin with <asp
are ASP.NET Server controls, and that is what I am talking about.

To see what these control do, press <F5>. Cassini launches, your Web
browser launches, and your new page appears. (See Figure 2-2).

A looks like the designer. There are some differences under the sheets.
Remember that Web browsers do not speak ASP.NET; they speak HTML. Your
Web server must translate our ASP.NET code into something that the Web
browser can understand. Here is that translation:

```
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN" "http://www.
w3.org/TR/html-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>title</title>
</head>
<body>
<form name="form" method="post" action="Default.aspx" id="form">
<div>
<input type="hidden" name="__VIEWSTATE" id="__VIEWSTATE" value="/
EFDW0UKmMTY40YDI3MWRkrf5c02juxUkkj5CIOHi77EU38=" />
</div>
</body>
</html>
```

*