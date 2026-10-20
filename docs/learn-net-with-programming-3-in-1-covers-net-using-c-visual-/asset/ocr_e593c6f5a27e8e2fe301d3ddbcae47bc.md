```
<td>User Name:</td><td> <asp:textbox id="user" runat="server"></asp:textbox></td>

<td><asp:requiredfieldvalidator ID="validuser" runat="server" controltovalidate="user" errormessage="Required!" forecolor="Red"></asp:requiredfieldvalidator></td>

</tr>

<tr>

<td>Password:</td><td><asp:textbox ID="pwd" runat="server" textmode="Password"></asp:textbox></td>

<td><asp:requiredfieldvalidator ID="validpwd" runat="server" controltovalidate="pwd" errormessage="Required!" forecolor="Red"></asp:requiredfieldvalidator></td>

</tr>

<tr>

<td>Confirm Password:</td><td><asp:textbox ID="Textbox1" runat="server" textmode="Password"></asp:textbox></td>

</tr>

<tr>
```