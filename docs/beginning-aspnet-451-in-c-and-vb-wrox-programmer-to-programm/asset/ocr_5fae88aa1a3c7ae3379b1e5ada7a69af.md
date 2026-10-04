CategoryId with a value of 10 and From with a value of the word Home. The page, Target.aspx (without an extension) in this example, is able to read these values using Request.QueryString. You see how to use the query string in the next exercise.

# TRY OUT Redirecting the User to Another Page

To give you a closer look at how it works, this exercise shows you how to create a page that redirects from one page to another using Response.Redirect. The example uses a temporary redirect (the page remains accessible after the redirect), so the code uses Response.redirect instead of Response.Redirect.

+   1. In the Demo folder, create two Web Forms based on your custom MyBasePage template. Call them Source.aspx and Target.aspx. Set their Title to Source and Target, respectively.
2. Source.aspx in Design View and double-click somewhere in the gray, red-only area of the page outside the ContentPlaceholder to set up a Page handler. Inside this handler, write the following code that redirects the user to the Target.aspx page. To show how to pass additional data through the query string and how to read information in the target page, the code passes a query string field Test with SomeValue as the value:
3. Target.aspx, switch to Design View, and add a Label control to the cpMainContent control. Leave its ID to Label1. Set up a Page handler similar to the one you created in the previous step by double-clicking the gray, red-only area of the page, and then add created in the following code:
4. Save all your changes, go back to Source.aspx, and press Ctrl+F5 to open it in the browser. Instead of seeing Source.aspx, you now see the page depicted in Figure 7-12.

```
VB.NET
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
Response.Redirect("Target?Test=SomeValue")
```

```
C#nprotected void Page_Load(object sender, EventArgs e)
{
    Response.Redirect("Target?Test=SomeValue");
}
```

```
VB.NET
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
Label1.Text = Request.QueryString.ToString()
```

```
C#nprotected void Page_Load(object sender, EventArgs e)
{
    Label1.Text = Request.QueryString.ToString();
}
```