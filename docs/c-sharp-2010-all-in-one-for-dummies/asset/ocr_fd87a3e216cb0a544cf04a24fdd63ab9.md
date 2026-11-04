Why not make it easy on yourself later on down the road?

If you decide which parts of the application are most likely to have problems while you code, you can insert trace messages as you go. It seems like a defeatist attitude, but, really I think it is a realist attitude. Even if it is just caused by bad data in two years, you are probably going to spend some time debugging.

To use tracing, you can alter the @Page statement at the top of each page in the application, or you can alter the Web.config file — which is what we are gonna do. If you want to set up the whole site for tracing, just add the bold code below to the Web.Config:

```
```xml
<configuration>
  <system.web>
    <trace enabled="true" requestLimit="40" localOnly="false" />
  </system.web>
</configuration>
```
```

Follow these steps to alter the Web.config file for tracing:

+   1. **Create a new page in the project for tracing.**
+      I called it Tracing.aspx.
+   
+   2. **Add the Trace statement to the @page directive of the new Tracing.aspx page.**
+   
+   3. **In the code-behind, add the code to the Page_Load event handler to fake an exception and catch it, and then write to the Trace.**

```
```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Tracing.aspx.cs" Inherits="Chapter_4.Tracing" Trace="true" %>
```
```

This is just to see how Trace works. Book 1 covers Exception handling in more detail.

```
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace Chapter_4
{
    public partial class Tracing : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            try
            {
                throw new ApplicationException("This is the fake exception.");
            }
```
```