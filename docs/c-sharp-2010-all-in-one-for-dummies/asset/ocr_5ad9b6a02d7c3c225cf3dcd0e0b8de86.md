+   3. Uncheck the box in Step 2 so that you don't build a code-behind file.
+   4. Name your file and press OK.

I named mine InlineCode.

Figure 2-7:
Adding inline code.

![](bbox=[0.3, 0.3, 0.7, 0.6])

That's all there is to it, one check box.

What you have now is practically the same thing as the code-behind version, except no ASPX.CS file. Instead you have a <script> block in the markup code, which looks like this:

```
<%@ Page Language="C#" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<script runat="server">

</script>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
</div>
</form>
</body>
</html>
```