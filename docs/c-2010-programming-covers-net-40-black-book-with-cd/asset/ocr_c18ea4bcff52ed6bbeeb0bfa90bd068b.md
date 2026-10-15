# # Chapter 14: Standard Web Server Controls

```
<br />
<asp:Label ID="Label2" runat="server"></asp:Label>
<br />
<br />
<br />
<br />
</div>
</form>
</body>
</html>
```

Now, add the code, shown in Listing 14.9, in the code-behind file of the Default.aspx page for the HiddenField controls:

# ## Listing 14.9: Showing the Code for the Code-behind File of the Default.aspx Page

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        HiddenField1.Value = "Welcome to the World of ASP.NET 4.0";
    }
    protected void Button1_Click(object sender, EventArgs e)
    {
        Label2.Text = HiddenField1.Value;
    }
}
```

Now, run the application by pressing the F5 key. The output is shown in Figure 14.5:

![](bbox=[0.05, 0.86, 0.95, 0.98])

# Figure 14.5: Showing a Value of the HiddenField Control on the Button Click Event