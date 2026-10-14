# A content page with a ScriptManagerProxy control

![](bbox=[0.155, 0.108, 0.856, 0.431])

# The aspx code for the ScriptManagerProxy control

```
```aspx
<asp:ScriptManagerProxy ID="ScriptManagerProxy1" runat="server">
</asp:ScriptManagerProxy>
```
```

# Aspx code for a ScriptManagerProxy control that registers scripts

```
```aspx
<asp:ScriptManagerProxy ID="ScriptManager1" runat="server">
    <Scripts>
        <asp:ScriptReference Path="~/Scripts/SampleScript.js" />
        <asp:ScriptReference Assembly="SampleAssembly"
            Name="SampleAssembly.SampleScript.js" />
    </Scripts>
</asp:ScriptManagerProxy>
```
```

# Aspx code for a ScriptManagerProxy control that registers a WCF service

```
```aspx
<asp:ScriptManagerProxy ID="ScriptManager1" runat="server">
    <Services>
        <asp:ServiceReference
            Path="http://www.example.com/Services/SampleService.svc" />
    </Services>
</asp:ScriptManagerProxy>
```
```

# Description

+   - The ScriptManagerProxy control lets you extend the scripting services that are provided by a ScriptManager control. It’s used most often on a content page whose master page contains a ScriptManager control.
+   - You can have multiple ScriptManagerProxy controls on a page. However, the ScriptManagerProxy controls can’t override the properties of the ScriptManager control.

Figure 21-7  How to use the ScriptManagerProxy control