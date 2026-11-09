You can also set the value of the `VaryByParam` attribute to `*`, which directs the caching engine to check any POST parameter associated with the requests.

# Implementing Output Caching

Output caching is the simplest method of caching available in ASP.NET. To show how to implement output caching in Web pages, let’s create a new Web site by performing the following steps:

+   1. *Open* **Microsoft Visual Studio 2010**.
+   2. *Click* **File > New > Web Site**. The New Web Site dialog box appears.
+   3. *Select* **Visual C#** from the **Installed Templates** pane and the **ASP.NET Web Site** template from the middle pane of the **New Web Site** dialog box and name it as **OutputCache**.
+   4. *Click* the **OK** button.
+      The OutputCache application (also available on the CD) has been created.
+   5. *Add* the following code snippet under the **@Page** directive of the **Default.aspx** page:

```
<%@ OutputCache Duration="10" VaryByParam="none" %>
```

+   6. *Select* the **Design** tab to view the design of the Web page.
+   7. *Drag* and drop three **Label** controls on the **Default.aspx** page from the Toolbox.
+   8. *Right-click* each control, select the **Properties** option from the context menu to open the **Properties** window. Set the properties of each control, as listed in Table 9.6.

| Table 9.6: Properties to be Set for the Controls |  |  |
|---|---|---|
| **Control Name** | **Property Name** | **Value** |
| Label1 | Text | Output Cache example |
| Label3 | Text | The above displayed time was cached for 10 seconds. Keep refreshing the Web page to see the changes. |

+   9. *Rearrange* the **Label** controls in the **Default.aspx** page, as shown in Fig. ASP-9.1:

![](bbox=[0.293, 0.527, 0.729, 0.775])

Fig. ASP-9.1

+   10. *Double-click* the **Default.aspx.cs** file in the Solution Explorer window to open it (Fig. ASP-9.1). Now, *add* the code, shown in Listing 9.1, in the **Page_Load** event of the **Default.aspx** page:

# Listing 9.1: Showing the Code for the Page_Load Event

```
using System;
using System.Collections.Generic;
```