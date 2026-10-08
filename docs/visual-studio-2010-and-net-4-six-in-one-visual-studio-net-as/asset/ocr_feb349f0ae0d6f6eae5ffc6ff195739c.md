+   - MicrosoftAjaxNetwork.js
- MicrosoftAjaxWebForms.js
- MicrosoftAjaxWebServices.js
- MicrosoftAjaxApplicationServices.js
- MicrosoftAjaxTemplates.js (new for ASP.NET Ajax 4)
- MicrosoftAjaxAdoNet.js (new for ASP.NET Ajax 4)

Figure 19-3 shows the dependencies between the split scripts.

![](bbox=[0.146, 0.305, 0.656, 0.671])

**Figure 19-3:** Microsoft Ajax Library scripts and their dependencies

As an example, if you would like to call the TimeServer.asm web service, but you do not use templates, globalization, history, and so on, then you can configure the ScriptManager like this:

```
<asp:ScriptManager ID="ScriptManager" runat="server"
    EnablePartialRendering="False"
    AjaxMode="Explicit">
    <CompositeScript>
        <Scripts>
            <asp:ScriptReference Name="MicrosoftAjaxCore.js" />
            <asp:ScriptReference Name="MicrosoftAjaxSerialization.js" />
            <asp:ScriptReference Name="MicrosoftAjaxNetwork.js" />
            <asp:ScriptReference Name="MicrosoftAjaxWebServices.js" />
        </Scripts>
    </CompositeScript>
</asp:ScriptManager>
```