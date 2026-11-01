```
VB.NET
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    Response.Redirect("Target.aspx?Test=SomeValue")
End Sub
```

```
C#
protected void Page_Load(object sender, EventArgs e)
{
    Response.Redirect("Target.aspx?Test=SomeValue");
}
```

3. Open Target.aspx, switch to Design View, and add a Label control to the cpMainContent Content control. Leave its ID set to Label1. Set up a Page_Load handler similar to the one you created in the previous step by double-clicking the gray, read-only area of the page, and then add the following code:

```
VB.NET
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    Label1.Text = Request.QueryString.ToString()
End Sub
```

```
C#
protected void Page_Load(object sender, EventArgs e)
{
    Label1.Text = Request.QueryString.ToString();
}
```

4. Save all your changes, go back to Source.aspx, and press Ctrl+F5 to open it in the browser. Instead of seeing Source.aspx, you now see the page depicted in Figure 7-12.

![](bbox=[0.1, 0.86, 0.9, 0.96])

FIGURE 7-12

Note that the address bar now reads Target.aspx?Test=SomeValue, the page you redirected to in the Page_Load event handler of the source page. The Label in the target page shows the query string that is passed to this page. Notice that QueryString.ToString() contains only Test=SomeValue. The address and the question mark are not a part of the query string for the page.