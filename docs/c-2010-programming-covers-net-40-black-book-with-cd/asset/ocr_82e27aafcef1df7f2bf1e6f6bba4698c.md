> NOTE
> These properties are not used by the Web Parts control set when rendering a DeclarativeCatalogPart control. The property is overridden only for the purpose of preventing it from appearing in Microsoft Visual Studio 2010 designer tools.

# The PageCatalogPart Control

The PageCatalogPart control is used with the CatalogZone control to add a specific functionality to the catalog section of a Web page. This control allows users to restore previously deleted WebPart controls of a Web page. This is the only way users have to restore the deleted Web Parts controls. The PageCatalogPart control adds a list of check boxes to the catalog zone controls corresponding to each deleted Web Parts control. To restore these controls on the Web page, users simply need to select the required check box and a Web part zone where the Web Parts control is to be added, and click the Add button.

To add the PageCatalogPart control to the CatalogZone control, drag and drop the PageCatalogPart control from the Toolbox to the CatalogZone control in the Design view of a Default.aspx page. Figure 16.14 shows the PageCatalogPart control inside the CatalogZone control in the Design view:

![](bbox=[0.1, 0.37, 0.9, 0.55])

Figure 16.14: Displaying the PageCatalogPart Control

```
<asp:CatalogZone ID="CatalogZone1" runat="server" Height="183px" width="318px">
<ZoneTemplate>
<asp:PageCatalogPart ID="PageCatalogPart1" runat="server" Height="198px" />
</ZoneTemplate>
</asp:CatalogZone>
```

The PageCatalogPart control is an object of the PageCatalogPart class. This control is associated to the PageCatalogPart class, which provides the same events, methods, and properties as those provided by the CatalogZone class.

+   System.Object
+   System.Web.UI.Control
+   System.Web.UI.WebControls.WebControl
+   System.Web.UI.WebControls.Panel
+   System.Web.UI.WebControls.WebPart
+   System.Web.UI.WebControls.WebParts.CatalogPart
+   System.Web.UI.WebControls.WebParts.PageCatalogPart

You can declare the PageCatalogPart class to add a PageCatalogPart control. The syntax to declare the PageCatalogPart class is given as follows:

```
PageCatalogPart pagecatalogpart;
```

# The ImportCatalogPart Control

The ImportCatalogPart control imports the description file of a Web Parts control or server control that is used as a Web Parts control. This enables the server control to be added to a Web page with pre-assigned settings. The description file enables users to share the settings of Web PartsCatalogPart and the ImportCatalogPart control is the third control (the other two being DeclarativeCatalogPart and