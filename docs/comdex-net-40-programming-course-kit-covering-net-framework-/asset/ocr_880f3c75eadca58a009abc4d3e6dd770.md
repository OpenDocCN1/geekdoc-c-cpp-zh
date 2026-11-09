```
```aspx
<asp:Label ID="Label1" runat="server" Text="welcome to Theme Example">
</asp:Label>
<br />
<br />
<asp:Label ID="Label2" runat="server" Text="Enter your Name"></asp:Label>
<br />
<br />
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
<br />
<br />
<asp:Button ID="Button1" runat="server" Text="Submit" />
</div>
</form>
</body>
</html>
```
```

In Listing 8.9, we have added two Label, one TextBox, and one Button controls to the Default.aspx page.

+   17. Apply the theme to the Default.aspx page by using the Theme attribute in the @ Page directive of the Default.aspx page, as shown in the following code snippet:

```
```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" Theme="Theme1" %>
```
```

The preceding code snippet adds the **Theme1** theme to the Default.aspx page.

The style properties of the skin file are not visible at design time. Therefore, to view the style of your page, which you have defined in the Look.skin file, you need to run the website.

+   18. Press the F5 key to run your website and enter the text in the TextBox1 control. The output is shown in Fig.ASP-8.20:

![](bbox=[0.354, 0.463, 0.668, 0.646])

*Fig.ASP-8.20*

In Fig.ASP-8.20, the style properties that we have defined in the Look.skin file are incorporated in the controls of the Default.aspx page.

Let’s now learn how to apply themes on controls at runtime.

# Applying Themes on Controls at Runtime

In the previous section, you have learned to create a theme and apply it to the Web page level. Apart from the page level, you can also apply a theme at the control level. It is important to note that only the controls whose EnableTheming and Theme properties are set can inherit properties defined in the specified theme. The sample TextBox1 control declaration that applies a theme is as follows:

```
```aspx
<asp:TextBox ID="TextBox1" runat="server" EnableTheming="true" />
```
```

![](bbox=[0.215, 0.812, 0.277, 0.851])

**You can also create multiple themes and give a choice to the user to apply any theme at runtime.**