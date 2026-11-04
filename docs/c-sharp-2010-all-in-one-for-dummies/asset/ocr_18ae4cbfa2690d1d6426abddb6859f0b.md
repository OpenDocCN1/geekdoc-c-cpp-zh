Note also that there is a language declaration at the top of the page rather than an InheritsFrom. This is because you are no longer building a DLL file but are just interpreting this all at runtime.

Go back to Design view, add a button, and double-click on it in the designer. You return to Source view rather than Code View, because there is no Code View. The event handler is now in the <script> block, as shown:

```
```aspx
<%@ Page Language="C#" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<script runat="server">

    protected void Button1_Click(object sender, EventArgs e)
    {
    }
</script>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <div>

        <asp:Button ID="Button1" runat="server"
        onclick="Button1_Click" Text="Button" />

    </div>
    </form>
</body>
</html>
```
```

That's really about it. It looks and works a lot like Active Server Pages. Sometimes you might need to use it so it is valuable to understand how to do it.

# ### Building in n-tier

Going the opposite direction from inline code, I have what used to be called n-tier code, but now it's called a hundred different things. At the essence here, I am talking about purposefully dividing the code of the application up into DLLs, instead of just having Visual Studio do it for you.