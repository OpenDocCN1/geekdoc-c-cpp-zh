+   11. Click the Button in the designer.
+       The Properties panel changes to show the button’s properties.
+   12. Change the Text property to Click Me.
+   13. Change the (ID) to ChangeText.

Now change back to Source view and note the changes in the code:

```
~~~
<%@ Page Language="VB" AutoEventWireup="false"
    CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" >
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <div>

        <asp:Label ID="TextToChange" runat="server" Font-
Size="14pt" Text="Label">Text to change</asp:Label>
        <br />
        <asp:Button ID="ChangeText" runat="server"
Text="Click Me" />

    </div>
    </form>
</body>
</html>
~~~
```

So the management of your code is what the designer does for you. Now, some people don't like Visual Studio messing with their code. Some people don't like to remember all the ins and outs of ASP.NET. It's all up to you; you can use it or not.

This isn't where the magic is, though. This is a C# book, and if you are working in a big shop your ASP.NET code is probably being written for you anyway. You want to play with the server code, and I don't blame you.

# ### Coding in Code View

If you go back to the design view and double-click on the Button control you dragged over, you will see something a little more familiar than all of this crazy markup. Usually called the code-behind, this is the C# code that makes the form manageable by the server. This code should look like this: