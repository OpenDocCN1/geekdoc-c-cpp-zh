```
</form>
</body>
</html>
```

Next, open the Default.aspx.cs file and add the code shown in Listing 16.16 to it:

# Listing 16.16: Code of the Default.aspx.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Web.UI.WebControls.WebParts;
public partial class _Default : System.Web.UI.Page
{
    WebPartManager wpm = new WebPartManager();
    EditorZone ez = new EditorZone();
    protected void Page_Load(object sender, EventArgs e)
    {
        Label1.Text = WebPartManager.EditDisplayMode.Name;
    }
    protected void Button1_Click(object sender, EventArgs e)
    {
        String str;
        String str1;
        str = ez.EmptyZoneText;
        Label2.Text = str;
        str1 = ez.HeaderText;
        Label3.Text = str1;
    }
}
```

To run the EditorZoneControl Web application, press the F5 key and click the Default Values button. You get the output as shown in Figure 16.51:

![](bbox=[0.22, 0.56, 0.78, 0.9])

Figure 16.51: Output of EditorZoneControl Web Application