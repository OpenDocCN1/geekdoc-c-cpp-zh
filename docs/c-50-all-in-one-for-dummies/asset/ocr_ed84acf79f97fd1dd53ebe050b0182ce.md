# 702 Constructing User Controls

![](bbox=[0.238, 0.125, 0.855, 0.463])

Figure 3-10: The Phone Number control.

+   4. Add a label and a button to the form; try to fill the control, click the button, and see the formatted phone number.

+   5. Double-click the button in Design View to get an event handler for the click event; add some code to populate the label on the button click, like this:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace Chapter_3
{
    public partial class UseThePhoneNumber : System.Web.UI.Page
    {
        protected void Button_Click(object sender, EventArgs e)
        {
            Label1.Text = PhoneNumber1.PhoneNumber;
        }
    }
}
```

+   6. Right-click the ASPX page and set it as the start page.

+   7. Press <F5> and run the application.

+   8. Enter a phone number in the control and click the button.

The formatted phone number should appear in the label.