```
<asp:TemplateField HeaderText="Summary" SortExpression="Summary">
    <EditItemTemplate>
        <asp:TextBox ID="TextBox2" TextMode="MultiLine" Width="500" Height="100" runat="server" Text='<%# Bind("Summary") %>'></asp:TextBox>
    </EditItemTemplate>
    <InsertItemTemplate>
        <asp:TextBox ID="TextBox2" TextMode="MultiLine" Width="500" Height="100" runat="server" Text='<%# Bind("Summary") %>'></asp:TextBox>
    </InsertItemTemplate>
</asp:TemplateField>
```

4. Add a RequiredFieldValidator in the EditItemTemplate and the InsertItemTemplate of both the Title and the Summary rows. You can drag and drop it from the Toolbox directly in Markup View or enter the required code manually. Using a code snippet makes this even easier: position your mouse on an empty, new line below the TextBox, type requiredfieldvalidator, and press Tab. VS inserts a RequiredFieldValidator for you and automatically assigns the ControlToValidate property with the ID of the previous TextBox defined in the code.

Make sure you hook up all validators to their respective TextBox controls in the template by setting the ControlToValidate property and providing a useful error message. When you're done, the summary field should look like this:

```
<asp:TemplateField HeaderText="Summary" SortExpression="Summary">
    <EditItemTemplate>
        <asp:TextBox ID="TextBox2" TextMode="MultiLine" Width="500" Height="100" runat="server" Text='<%# Bind("Summary") %>'></asp:TextBox>
        <asp:RequiredFieldValidator ControlToValidate="TextBox2" runat="server" ErrorMessage="Enter a summary" />
    </EditItemTemplate>
    <InsertItemTemplate>
        <asp:TextBox ID="TextBox2" TextMode="MultiLine" Width="500" Height="100" runat="server" Text='<%# Bind("Summary") %>'></asp:TextBox>
        <asp:RequiredFieldValidator ControlToValidate="TextBox2" runat="server" ErrorMessage="Enter a summary" />
    </InsertItemTemplate>
</asp:templatefield>
```

The Title and Body fields should look similar to Summary. The TextBox for the Title field doesn't have the TextMode, Width, and Height properties applied, whereas the Body field is missing the RequiredFieldValidator. Other than that, the fields should look pretty similar to the Summary field.

5. Switch to Design View and drag a new SqlDataSource control next to SqlDataSource1 that is already on the page. Open the new control's Smart Tasks panel and click Configure Data Source. Select the Planet Wrox connection string from the drop-down list and click Next. Select the Id and Name columns from the Genre table and set up an ORDER BY clause on the SortOrder column by clicking the ORDER BY button and choosing SortOrder from the Sort By drop-down list. When you click OK, the Configure Data Source screen looks like Figure 13-19.