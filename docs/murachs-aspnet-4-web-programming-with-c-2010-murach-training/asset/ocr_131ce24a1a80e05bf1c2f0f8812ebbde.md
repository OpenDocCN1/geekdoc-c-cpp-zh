# Some of the C# code for the Cart page

```
public partial class Cart : System.Web.UI.Page
{
    .
    .
    protected void btnCheckOut_Click(object sender, EventArgs e)
    {
        string url = "https:"
            + ConfigurationManager.AppSettings["AppPath"]
            + "Checkout1.aspx";
        Response.Redirect(url);
    }
}
```

# Some of the C# code for the first Check Out page

```
public partial class Checkout1 : System.Web.UI.Page
{
    .
    .
    protected void Page_Load(object sender, EventArgs e)
    {
        if (!Request.IsSecureConnection)
        {
            string url = Request.Url.ToString().Replace("http:", "https:");
            Response.Redirect(url);
        }
    }

    protected void btnCheckOut_Click(object sender, EventArgs e)
    {
        if (Page.IsValid)
        {
            .
            .
            Response.Redirect("Checkout2.aspx");
        }
    }

    protected void btnCancel_Click(object sender, EventArgs e)
    {
        Session.Remove("Cart");
        String url = "http:"
            + ConfigurationManager.AppSettings["AppPath"]
            + "Order.aspx";
        Response.Redirect(url);
    }

    protected void btnContinue_Click(object sender, EventArgs e)
    {
        string url = "http:"
            + ConfigurationManager.AppSettings["AppPath"]
            + "Order.aspx";
        Response.Redirect(url);
    }
}
```