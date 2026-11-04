Change to the Source view, back where you started. Check out the designer
source and I'll break down the ASP.NET code from the HTML code a little bit.
Here is the code after the controls are added:

```
~~~html
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Default.aspx.cs"
    Inherits="AspNetFirstSample._Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.
    w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" >
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <div>

            <asp:Label ID="Label1" runat="server" Text="Label"></asp:Label>

        </div>
        <p>
            <asp:Button ID="Button1" runat="server" Text="Button" />
        </p>
    </form>
</body>
</html>
~~~
```

If you have any experience with HTML, you recognize 90 percent of what is
on the screen. <html>, <head>, <body>, and <form> are all common HTML
tags that you can find on any Web page. The two tags that begin with <asp
are ASP.NET Server controls, and that is what I am talking about here.

To see what these controls do, press <F5>. Cassini launches, your Web
browser launches, and your new page appears. (See Figure 2-2.)

Looks a lot like the designer. There are some differences under the sheets.
Remember that Web browsers don't speak ASP.NET; they speak HTML. Your
Web server must translate our ASP.NET code into something that the Web
browser can use. Here is that translation:

```
~~~html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.
    w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" >
<head><title>

</title></head>
<body>
    <form name="form1" method="post" action="Default.aspx" id="form1">
        <div>
            <input type="hidden" name="__VIEWSTATE" id="__VIEWSTATE" value="
            wEPDwUKMTI2NTY4ODI3MWhkF5c0Gg2jXU1kj5C1oHCiRot7EU38e" />
~~~
```