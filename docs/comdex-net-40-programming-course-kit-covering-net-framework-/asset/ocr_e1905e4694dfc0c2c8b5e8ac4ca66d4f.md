The PageCatalogPart control provides a list of check boxes of closed WebParts controls. To open or add these closed WebParts controls again to the Web page, select the check boxes as well as the zone where the controls have to be added and then click the Add button in the PageCatalogPart control on the Web page.

+   - **ImportCatalog:** Helps users to import the description file (the `.WebPart` file) for a WebParts control. The `.WebPart` file describes the settings of WebParts controls, which can be added to a specified zone on a Web page. The control provides the facility to browse and upload the `.WebPart` file.

You can insert the CatalogZone control on the Design view of the Web Form by performing the following steps:

+   1. Click **Start→All Programs→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010**.
+   2. Select **File→New→Web Site** from the menu bar.
+      The New Web Site dialog box appears.
+   3. Select **Visual C#→ASP.NET Web Site** in the middle Templates pane.
+   4. Set the name of the Web site as **CatalogzoneControl**.
+   5. Click the **OK** button.
+      The **CatalogzoneControl** application is created.
+   6. Drag and drop the CatalogZone control from the **WebParts** tab in the Toolbox.

In Fig.ASP-7.2, you can see that the CatalogZone control gets added on the Design view of the **Default.aspx** page:

![](bbox=[0.275, 0.442, 0.748, 0.725])

Fig.ASP-7.2

After learning about CatalogZone control, let’s now learn about WebPartZone control.

# ## Using the WebPartZone Control

The **WebPartZone** control is a control that is used to describe a region on a WebParts page for placing the WebParts or other controls, such as **Label, Textbox,** and **Image** controls. Once placed, the controls can be relocated, maximized, or minimized according to the requirements of the end-user. The **WebPartZone** control resides within the `System.Web.UI.WebControls.WebParts` namespace.