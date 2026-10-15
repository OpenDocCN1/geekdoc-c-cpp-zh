
3. Next, open the Default.aspx file and replace the existing code with the code shown in Listing 16.18:

# Listing 16.18: Code of the Default.aspx File

```
<asp:TextBox ID="TextBox1" Runat="server" />
<br />
<asp:Button ID="Button1" Text="Button" Runat="server" />
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<%@ Register TagPrefix="cc" TagName="customcontrol" Src="customcontrol.ascx" %>
<script runat="server">
protected void Page_Load(object sender, EventArgs e)
{
    if (WebPartManager1.Personalization.CanEnterSharedScope && WebPartManager1.Personalization.Scope == PersonalizationScope.User)
    {
        WebPartManager1.Personalization.ToggleScope();
    }
}
protected void LinkButton1_Click(object sender, EventArgs e)
{
    WebPartManager1.DisplayMode = WebPartManager.EditDisplayMode;
}
protected void LinkButton2_Click(object sender, EventArgs e)
{
    WebPartManager1.DisplayMode = WebPartManager.BrowseDisplayMode;
}
</script>
<html>
<head id="Head1" runat="server">
<title>custom control</title>
</head>
<body>
<form id="form1" runat="server">
    <div id="header"><h1>C# 2010 Black Book</h1></div>
    <div id="content">
        <asp:WebPartManager ID="WebPartManager1" runat="server" />
        Custom WebPart &nbsp;<br />
        <asp:LinkButton ID="LinkButton1" runat="server" OnClick="LinkButton1_Click">Edit Mode</asp:LinkButton>
        <asp:LinkButton ID="LinkButton2" runat="server" OnClick="LinkButton2_Click">Browse Mode</asp:LinkButton><br /><br />
        <asp:WebPartZone ID="WebPartZone2" runat="server">
        <ZoneTemplate>
        <cc:customcontrol runat="server" id="customcontrol1" />
        </ZoneTemplate></asp:WebPartZone>
        <asp:EditorZone ID="EditorZone1" runat="server" BackColor="#F7F6F3" BorderColor="#CCCCCC" BorderWidth="1px" Font-Names="verdana" Padding="6">
        <LabelStyle Font-Size="0.8em" ForeColor="#333333" />
        <HeaderStyle BackColor="#E2DED6"
```

```
Font-Bold="True" Font-Size="0.8em"
ForeColor="#333333" /> <ZoneTemplate>
<asp:BehaviorEditorPart
ID="BehaviorEditorPart1" runat="server" />
<asp:LayoutEditorPart
ID="LayoutEditorPart1" runat="server"  />
</ZoneTemplate>
<HeaderVerbStyle Font-Bold="False"
Font-Size="0.8em" Font-Underline="False"
ForeColor="#333333" />
<PartChromeStyle
BorderColor="#E2DED6" BorderStyle="Solid" BorderWidth="1px" />
<PartStyle
BorderColor="#F7F6F3" BorderWidth="5px" />
<FooterStyle BackColor="#E2DED6"
HorizontalAlign="Right" />
<EditUIStyle Font-Names="Verdana"
Font-Size="0.8em" ForeColor="#333333" />
<InstructionTextStyle
Font-Size="0.8em" ForeColor="#333333" />
<ErrorStyle Font-Size="0.8em" />
<VerbStyle Font-Names="verdana"
Font-Size="0.8em" ForeColor="#333333" />
<EmptyZoneTextStyle
Font-Size="0.8em" ForeColor="#333333" />
<PartTitleStyle Font-Bold="True"
Font-Size="0.8em" ForeColor="#333333" />
</asp:EditorZone>
<br /><br /><br />
</div>
</form>
</body>
</html>
```

4. Now, add the following code inside the <system.web> section of the Web.config file:

```
<webParts>
<personalization>
<authorization>
<allow users="*" verbs="entersharedscope"/>
</authorization>
</personalization>
</webParts>
```

5. To run the CustomWebPart Web application, press the F5 key. Figure 16.52 shows the output:

![](img/e073a4882197be4ab61103cbe0bcb394_860_0.png)

Figure 16.52: The Output of CustomWebPart Web Application

6. Click the Edit Mode link (Figure 16.52) to switch to the Edit mode. Now, click the down arrow on Custom Control and select the Edit option, as shown in Figure 16.53:

![](img/e073a4882197be4ab61103cbe0bcb394_861_0.png)

When you select the Edit option, the Editor Zone appears on the Web page, as shown in Figure 16.54:

![](img/e073a4882197be4ab61103cbe0bcb394_861_1.png)

As you can see in Figure 16.54, the Editor Zone contains various editor parts that allow you to modify the appearance and layout of the custom Web Parts control. As per your requirements, you can modify the properties of the custom Web Parts control by selecting the appropriate options from the Editor Zone control, and then click the Apply button. Finally, click the OK button to apply the changes to the custom Web Part control.

## Creating the ConnectionsZone Control in Code

We discussed the working of the ConnectionsZone control in the In Depth section of this chapter. We also discussed how to use the ConnectionsZone class to create the ConnectionsZone control. Now, let's create the ConnectionsZone control with the help of the ConnectionsZone class and specify the various properties of the control. For this, we create an application named ConnectionsZoneApp (also available in the CD). Listing 16.19 shows the complete code for the Default.aspx page of the ConnectionsZoneApp website:

### Listing 16.19: Showing the Code for the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>ConnectionsZone control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label2" runat="server" Font-Bold="True" Font-Underline="True" ForeColor="Navy" Text="ConnectionZone Webpart:"></asp:Label>
<br />
<br />
<asp:Panel ID="Panel1" runat="server" BackColor="#FFE0C0" BorderStyle="Ridge" Height="161px" Width="437px">
<asp:Label ID="Label1" runat="server" Text="Connection Status:" Width="622px" Font-Bold="True" Font-Underline="True" ForeColor="Navy"></asp:Label><br />
&nbsp;<asp:Label ID="Label3" runat="server" Text="Label"></asp:Label>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<asp:Label ID="Label5" runat="server" Font-Bold="True" Font-Underline="True" ForeColor="Navy" Text="Connection Configuration:"></asp:Label>
<br />
<br />
<asp:Label ID="Label4" runat="server" Text="Label"></asp:Label>&nbsp;
<br />
<asp:Label ID="Label6" runat="server" Text="Label"></asp:Label></asp:Panel>
</div>
</form>
</body>
</html>
```

### Listing 16.20: Showing the Code for the Code-Behind File of the Default.aspx Page

```
using System;
using System.Configuration;
using System.Data;
using System.Linq;
using System.Web;
using System.Web.Security;
using System.Web.UI;
using System.Web.UI.HtmlControls;
using System.Web.UI.WebControls;
using System.Web.UI.WebControls.WebParts;
using System.Xml.Linq;
public partial class _Default : System.Web.UI.Page
{
    WebPartManager wpm = new WebPartManager();
    ConnectionsZone conn = new ConnectionsZone();
    protected void Page_Load(object sender, EventArgs e)
    {
        string value;
        value = conn.NoExistingConnectionInstructionText;
        conn.NoExistingConnectionInstructionText = value;
        Label13.Text = conn.NoExistingConnectionInstructionText;
        Label14.Text = "DEFAULT:" + conn.ConfigureConnectionTitle;
        conn.ConfigureConnectionTitle = "Configure a new connection";
        Label16.Text = "CUSTOM:" + conn.ConfigureConnectionTitle;
    }
}
```

Figure 16.55 shows the output of the ConnectionsZoneApp website:

![](img/e073a4882197be4ab61103cbe0bcb394_863_0.png)

Figure 16.55: Displaying the ConnectionsZone Control in Action

## Summary

In this chapter, we discussed about Login controls and their use to create and work with a user account. These controls include Login, LoginView, LoginStatus, LoginName, CreateUserWizard, Password, and ChangePassword. We also discussed about Web Parts controls that show how users can personalize their websites dynamically at runtime. These controls include WebPartManager, ProxyWebPartManager, WebPartZone, CatalogZone, and EditorZone control.

In the next chapter, you learn how to enhance Web applications with the help of Silverlight.
