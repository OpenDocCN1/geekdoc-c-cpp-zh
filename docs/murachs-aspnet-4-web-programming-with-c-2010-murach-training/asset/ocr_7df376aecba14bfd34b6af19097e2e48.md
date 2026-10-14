# The Default.aspx file

```
<p id="new">To create a new category, enter the category information and click Add New Category.</p>
<p>
<asp:Label ID="lblError" runat="server" EnableViewState="False" CssClass="error">
</asp:Label>
</p>
<p class="label">ID:</p>
<p class="entry">
<asp:TextBox ID="txtID" runat="server" Width="100" MaxLength="10">
</asp:TextBox>&nbsp;
<asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server" ControlToValidate="txtID" CssClass="error" ErrorMessage="ID is a required field.">
</asp:RequiredFieldValidator>
</p>
<p class="label">Short Name:</p>
<p class="entry">
<asp:TextBox ID="txtShortName" runat="server" Width="200" MaxLength="15">
</asp:TextBox>&nbsp;
<asp:RequiredFieldValidator ID="RequiredFieldValidator2" runat="server" ControlToValidate="txtShortName" CssClass="error" ErrorMessage="Short Name is a required field.">
</asp:RequiredFieldValidator>
</p>
<p class="label">Long Name:</p>
<p class="entry">
<asp:TextBox ID="txtLongName" runat="server" Width="200" MaxLength="50">
</asp:TextBox>&nbsp;
<asp:RequiredFieldValidator ID="RequiredFieldValidator3" runat="server" ControlToValidate="txtLongName" CssClass="error" ErrorMessage="Long Name is a required field.">
</asp:RequiredFieldValidator>
</p>
<p>
<asp:Button ID="btnAdd" runat="server" Text="Add New Category" OnClick="btnAdd_Click" />
</p>
</div>
</div>
</form>
</body>
</html>
```

# Notes

+   - The text boxes are used to enter data for a new row.
+   - The required field validators ensure that the user enters data for each column of a new row.