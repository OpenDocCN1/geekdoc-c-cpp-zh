Now, we need to add the voting or polling functionality to the newly created Web user control. Switch to the Design mode and add the voting related controls, as shown below:

![](bbox=[0.21, 0.13, 0.84, 0.43])

Design View of WebUserControl.ascx

We’ll understand the significance of each of the controls present in the WebUserControl.ascx file later as we continue to develop this application. The following is the source code contained in the WebUserControl.ascx file:

```
<%@ Control Language="C#" AutoEventWireup="true" CodeFile="WebUserControl.ascx.cs" Inherits="WebUserControl" %>
<asp:Label ID="Label1" runat="server" Font-Size="Larger" Text="Do you like this Web site?"></asp:Label>&nbsp;<br />
<asp:RadioButtonList ID="RadioButtonList1" runat="server" OnSelectedIndexChanged="RadioButtonList1_SelectedIndexChanged">
<asp:ListItem Selected="true" Text="Yes" Value="yes"></asp:ListItem>
<asp:ListItem Selected="false" Text="No" Value="no"></asp:ListItem>
</asp:RadioButtonList>
<asp:Button ID="Button1" runat="server" OnClick="Button1_Click" Text="Vote" />
<asp:Label ID="Label4" runat="server" ForeColor="Black" Text="Label" Width="559px"></asp:Label><br />
<br />
<br />
<br />
<asp:Button ID="Button2" runat="server" OnClick="Button2_Click" Text="Click Here to View the Poll Results!!" /><br />
<br />
<br />
<asp:Label ID="Label2" runat="server" Text="Label"></asp:Label><br />
<asp:Label ID="Label3" runat="server" Text="Label"></asp:Label>
```

WebUserControl.ascx