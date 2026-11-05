![](bbox=[0.174, 0.095, 0.63, 0.441])

**Figure 15-15** Submit button clicked

![](bbox=[0.173, 0.51, 0.237, 0.562])

You might think the illustrations in Figure 15-15 are layered incorrectly, but they are not. As noted previously, Web pages are stateless. When the Submit button is clicked, a postback to the Web server occurs. When the page is redisplayed upon return from the round-trip to the server, the values in the text box are lost and not available for redisplay.

Adding the text box, button, and image controls to the form alters the code in the file containing the HTML (.aspx). It does not add any statements to the file ending in .aspx.cs (the code-behind file). The only statements that appear in the .aspx.cs file are those originally placed when the page was created. Example 15-4 shows the contents. Notice the number of namespaces imported automatically.

# Example 15-4

```
```csharp
// HtmlExample   Default.aspx.cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web;
using System.Web.UI.WebControls;
```
```