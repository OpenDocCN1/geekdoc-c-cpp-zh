```
<td>Email:</td><td><asp:textbox ID="email" runat="server" textmode="Email"></asp:textbox></td>

<td><asp:requiredfieldvalidator ID="validemail" runat="server" controltovalidate="email" errormessage="required!" forecolor="Red"></asp:requiredfieldvalidator></td>

</tr>

<tr>

<td>Mobile:</td><td><asp:textbox ID="mobile" runat="server" textmode="Phone"></asp:textbox></td>

</tr>

<tr>

<td>Gender:</td><td><asp:radiobuttonlist ID="radiobuttonlist1" runat="server">

<asp:listitem Text="Male" Value="0"></asp:listitem>

<asp:listitem Text="Female" Value="1"></asp:listitem>

</asp:radiobuttonlist></td>

</tr>

<tr>
```