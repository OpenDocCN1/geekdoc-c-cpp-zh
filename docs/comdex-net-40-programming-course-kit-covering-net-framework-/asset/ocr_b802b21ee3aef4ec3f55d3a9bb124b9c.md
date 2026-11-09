+   8. Add a skin file into the **Theme1** folder by right-clicking it and selecting the **Add New Item** option from the context menu.  
+      The **Add New Item** dialog box appears (Fig. ASP-8.19).  
+   9. Select the **Skin File** option from the middle pane of the **Add New Item** dialog box (Fig. ASP-8.19).  
+   10. Enter the name of the skin file in the **Name** text box. In our case, we have named the skin file as **Look.skin** (Fig. ASP-8.19).  
+   11. Click the **Add** button to add the file in the **Solution Explorer** window, as shown in Fig. ASP-8.19.

![](bbox=[0.289, 0.249, 0.734, 0.493])

Fig.ASP-8.19

The **Look.skin** file is added to the **Theme1** folder.

+   12. Add the code, shown in Listing 8.8, in the **Look.skin** file:

```
```aspx
<asp:label runat="server" width="350px" height="50px" font-bold="True"
    font-size="large" forecolor="Red" backcolor="Blue"/>
<asp:button runat="server" forecolor="white" backcolor="Black"/>
<asp:textbox runat="server" font-bold="True" font-size="medium" forecolor="Blue"
    backcolor="Silver" font-italic="True"/>
```
```

In Listing 8.8, we have defined the style properties for three controls, **Label**, **Button**, and **TextBox**.

+   13. Right-click the project name in **Solution Explorer** and select the **Add New Item** from the context menu. The **Add New Item** dialog box opens.  
+   14. Select the **Web Form** option from the middle pane of the **Add New Item** dialog box.  
+   15. Click the **Add** button to add the **Default.aspx** page to your project.  
+   16. Replace the code of the **Default.aspx** page with the code shown in Listing 8.9:

```
```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs"
    Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <div>
```
```