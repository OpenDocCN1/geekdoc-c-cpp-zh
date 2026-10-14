# The Default.aspx file

Page 3

```
<asp:CommandField ButtonType="Button"
    ShowDeleteButton="True"
    ShowEditButton="True"
    ShowInsertButton="True" />
</Fields>
<RowStyle BackColor="LightGray" ForeColor="Black" />
<EditRowStyle BackColor="Gray" ForeColor="White" />
<FooterStyle BackColor="LightGray" />
</asp:DetailsView>
<asp:SqlDataSource ID="SqlDataSource2" runat="server"
    ConflictDetection="CompareAllValues"
    ConnectionString="<%$ ConnectionStrings:HalloweenConnectionString %>"
    OldValuesParameterFormatString="original_{0}"
    SelectCommand="SELECT [ProductID], [Name], [ShortDescription],
        [LongDescription], [CategoryID], [ImageFile],
        [UnitPrice], [OnHand]
        FROM [Products]
        WHERE ([ProductID] = @ProductID)"
    DeleteCommand="DELETE FROM [Products]
        WHERE [ProductID] = @original_ProductID
            AND [Name] = @original_Name
            AND [ShortDescription] = @original_ShortDescription
            AND [LongDescription] = @original_LongDescription
            AND [CategoryID] = @original_CategoryID
            AND (([ImageFile] = @original_ImageFile)
                OR ([ImageFile] IS NULL AND @original_ImageFile IS NULL))
            AND [UnitPrice] = @original_UnitPrice
            AND [OnHand] = @original_OnHand"
    InsertCommand="INSERT INTO [Products] ([ProductID], [Name],
        [ShortDescription], [LongDescription], [CategoryID],
        [ImageFile], [UnitPrice], [OnHand])
        VALUES (@ProductID, @Name, @ShortDescription,
            @LongDescription, @CategoryID, @ImageFile,
            @UnitPrice, @OnHand)"
    UpdateCommand="UPDATE [Products] SET [Name] = @Name,
        [ShortDescription] = @ShortDescription,
        [LongDescription] = @LongDescription,
        [CategoryID] = @CategoryID,
        [ImageFile] = @ImageFile,
        [UnitPrice] = @UnitPrice,
        [OnHand] = @OnHand
        WHERE [ProductID] = @original_ProductID
            AND [Name] = @original_Name
            AND [ShortDescription] = @original_ShortDescription
            AND [LongDescription] = @original_LongDescription
            AND [CategoryID] = @original_CategoryID
            AND (([ImageFile] = @original_ImageFile)
                OR ([ImageFile] IS NULL AND @original_ImageFile IS NULL))
            AND [UnitPrice] = @original_UnitPrice
            AND [OnHand] = @original_OnHand">
    <SelectParameters>
        <asp:ControlParameter ControlID="GridView1" Name="ProductID"
            PropertyName="SelectedValue" Type="String" />
    </SelectParameters>
```