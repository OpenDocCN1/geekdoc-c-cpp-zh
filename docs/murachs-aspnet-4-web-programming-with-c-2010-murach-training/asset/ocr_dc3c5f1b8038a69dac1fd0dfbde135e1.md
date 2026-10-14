# The aspx file for the Order page (Order.aspx)

# Page 2

```
<tr>
    <td class="style2">
        <asp:Label ID="lblShortDescription" runat="server">
        </asp:Label>
    </td>
</tr>
<tr>
    <td class="style2">
        <asp:Label ID="lblLongDescription" runat="server">
        </asp:Label>
    </td>
</tr>
<tr>
    <td class="style2">
        <asp:Label ID="lblUnitPrice" runat="server" Font-Bold="True" Font-Size="Larger">
        </asp:Label>
        <asp:Label ID="Label2" runat="server" Text="each" Font-Bold="True" Font-Size="Larger">
        </asp:Label>
    </td>
</tr>
</table>
<br />
<asp:Label ID="Label13" runat="server" Text="Quantity:"></asp:Label>&nbsp;
<asp:TextBox ID="txtQuantity" runat="server" Width="40px">
</asp:TextBox>
<asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server" ControlToValidate="txtQuantity" Display="Dynamic" ErrorMessage="Quantity is a required field." ForeColor="Green">
</asp:RequiredFieldValidator>
<asp:RangeValidator ID="RangeValidator1" runat="server" ControlToValidate="txtQuantity" Display="Dynamic" ErrorMessage="Quantity must range from 1 to 500." MaximumValue="500" MinimumValue="1" Type="Integer" ForeColor="Green">
</asp:RangeValidator><br /><br />
<asp:Button ID="btnAdd" runat="server" Text="Add to Cart" OnClick="btnAdd_Click" />&nbsp;
<asp:Button ID="btnCart" runat="server" CausesValidation="False" PostBackUrl="~/Cart.aspx" Text="Go to Cart" />
</div>
</form>
</body>
</html>
```

# Description

+   - The txtQuantity text box lets the user enter the order quantity of the selected item. A RequiredFieldValidator and a RangeValidator are used to ensure that the user enters valid data in this text box.
+   - The OnClick attribute of the btnAdd button indicates that an event handler named btnAdd_Click will be executed when this button is clicked.
+   - The btnCart button uses cross-page posting to post to the Cart.aspx page.