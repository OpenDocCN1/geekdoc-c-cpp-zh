# Tracing with TraceContext 721

Follow these steps to alter the Web.config file for tracing:

+   1. Create a new page in the project for tracing.

I called it Tracing.aspx.

+   2. Add the Trace statement to the @page directive of the Tracing. aspx page.

```
<@ Language="C#" AutoEventWire="true" CodeBehind="Tracing.aspx.cs" Inherits="Chapter_4.Tracing" Trace="true" %>
```

+   3. In the code-behind, add code to the Page_Load event handler to fake an exception and catch it and write to the Trace.

This is just to see how Trace works. Book covers Exception handling in more detail.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.Controls;

namespace Chapter_4
{
    public partial class Tracing : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            try {
                throw new ApplicationException("This is the fake exception.");
            }
            catch (ApplicationException ex)
            {
                Trace.Warn(ex.Message);
            }
        }
    }
}
```

+   4. Press <F5> to run the application.

The page will look nothing like you expect. A ton of information is dumped on the page, Response.Write style, including the Trace message (check out Figure 4-4).

![](bbox=[0.883, 0.323, 0.963, 0.545])