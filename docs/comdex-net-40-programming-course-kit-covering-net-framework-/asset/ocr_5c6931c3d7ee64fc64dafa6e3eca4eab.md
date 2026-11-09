Perform the following steps to create and apply themes on controls at runtime:

+   1. Open Visual Studio 2010.
+   2. Select File→New→Web Site from the menu bar. The New Web Site dialog box opens.
+   3. Select Visual C# from the Installed Templates pane of the New Web Site dialog box.
+   4. Select ASP.NET Empty Web Site from the right pane of the New Web Site dialog box.
+   5. Specify the location and name of the application in the Web location combo box. In this case, we have specified the name as ApplyingThemesAtRuntime.
+   6. Click the OK button to create the ApplyingThemesAtRuntime application (also available on the CD).
+   7. Add the Theme1 folder in the App_Themes folder by right-clicking the ApplyingThemesAtRuntime project in Solution Explorer and selecting Add ASP.NET Folder→Theme from the context menu. Similarly, add another Theme folder, named Theme2, in the App_Themes folder.
+   8. Add the skin file to each theme folder by right-clicking the Theme1 folder and selecting the Add New Item option from the context menu. The Add New Item dialog box appears.
+   9. Select Skin File from the middle pane of the Add New Item dialog box.
+   10. Enter the name of the skin file in the Name text box. In our case, we have named the skin file as Simple.skin.
+   11. Click the Add button to add the skin file in the Theme1 folder.
+   12. Add the skin file to each theme folder by right-clicking the Theme2 folder and selecting the Add New Item option from the context menu. The Add New Item dialog box appears.

Perform steps 9 to 11 to add a Skin File, Inverse.skin, to the Theme2 folder.

+   13. Add the code, shown in Listing 8.10, in the Simple.skin file:

Listing 8.10: Showing the Code for the Simple.skin file

```
```
<asp:Label runat="server" width="350px" height="25px" font-bold="True"
font-size="Large" forecolor="Green" backcolor="Yellow"/>
<asp:button runat="server" forecolor="Green" backcolor="Yellow"/>
<asp:textbox runat="server" font-bold="True" font-size="Medium" forecolor="Blue"
backcolor="Silver" font-italic="True"/>
```
```

In Listing 8.10, we have defined the style properties for three controls, Label, Button, and TextBox.

+   14. Add the code, shown in Listing 8.11, in the Inverse.skin file:

Listing 8.11: Showing the Code for the Inverse.skin file

```
```
<asp:label runat="server" width="350px" height="50px" font-bold="True"
font-size="Large" forecolor="Blue" backcolor="Red"/>
<asp:button runat="server" forecolor="Silver" backcolor="Blue"/>
<asp:textbox runat="server" font-bold="True" font-size="Medium" forecolor="Silver"
backcolor="Blue" font-italic="True"/>
```
```

In Listing 8.11, we have defined the style properties for three controls, Label, Button, and TextBox.

+   15. Right-click the project name in Solution Explorer and select Add New Item from the context menu. The Add New Item dialog box opens.
+   16. Select the Web Form option from the middle pane of the Add New Item dialog box.
+   17. Click the Add button to add the Default.aspx page to your project.
+   18. Replace the code of the Default.aspx page with the code shown in Listing 8.12:

Listing 8.12: Showing the Code for Default.aspx of ApplyingThemesAtRuntime Application

```
```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs"
Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
```
```