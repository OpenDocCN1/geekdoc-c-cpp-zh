
## 产品维护窗体的代码

```
private MMABooksContext context = new MMABooksContext();
private Products selectedProduct;

private void frmProductMaintenance_Load(object sender, EventArgs e)
{
    DisplayProducts();
}

private void DisplayProducts()
{
    dgvProducts.Columns.Clear();

    var products = context.Products
        .OrderBy(p => p.Description)
        .Select(p => new { p.ProductCode, p.Description, p.UnitPrice })
        .ToList();

    dgvProducts.DataSource = products;

    // add column for modify button
    var modifyColumn = new DataGridViewButtonColumn() {
        UseColumnTextForButtonValue = true,
        HeaderText = "",
        Text = "Modify"
    };
    dgvProducts.Columns.Add(modifyColumn);

    // add column for delete button
    var deleteColumn = new DataGridViewButtonColumn() {
        UseColumnTextForButtonValue = true,
        HeaderText = "",
        Text = "Delete"
    };
    dgvProducts.Columns.Add(deleteColumn);

    // format the column headers
    dgvProducts.EnableHeadersVisualStyles = false;
    dgvProducts.ColumnHeadersDefaultCellStyle.Font =
        new Font("Arial", 9, FontStyle.Bold);
    dgvProducts.ColumnHeadersDefaultCellStyle.BackColor = Color.Goldenrod;
    dgvProducts.ColumnHeadersDefaultCellStyle.ForeColor = Color.White;

    // format the odd numbered rows
    dgvProducts.AlternatingRowsDefaultCellStyle.BackColor =
        Color.PaleGoldenrod;

    // format the first column
    dgvProducts.Columns[0].HeaderText = "Product Code";
    dgvProducts.Columns[0].Width = 110;

    // format the second column
    dgvProducts.Columns[1].Width = 310;

    // format the third column
    dgvProducts.Columns[2].HeaderText = "Unit Price";
    dgvProducts.Columns[2].HeaderCell.Style.Alignment = DataGridViewContentAlignment.MiddleRight;
    dgvProducts.Columns[2].Width = 90;
    dgvProducts.Columns[2].DefaultCellStyle.Format = "c";
    dgvProducts.Columns[2].DefaultCellStyle.Alignment = DataGridViewContentAlignment.MiddleRight;
}
```

```
private void dgvProducts_CellClick(object sender, DataGridViewCellEventArgs e)
{
    // store index values for Modify and Delete button columns
    const int ModifyIndex = 3;
    const int DeleteIndex = 4;

    if (e.ColumnIndex == ModifyIndex || e.ColumnIndex == DeleteIndex)
    {
        string productCode = dgvProducts.Rows[e.RowIndex].Cells[0].Value.ToString().Trim();
        selectedProduct = context.Products.Find(productCode);
    }

    if (e.ColumnIndex == ModifyIndex)
        ModifyProduct();
    else if (e.ColumnIndex == DeleteIndex)
        DeleteProduct();
}

private void ModifyProduct()
{
    var addModifyProductForm = new frmAddModifyProduct() {
        AddProduct = false,
        Product = selectedProduct
    };
    DialogResult result = addModifyProductForm.ShowDialog();
    if (result == DialogResult.OK)
    {
        try {
            selectedProduct = addModifyProductForm.Product;
            context.SaveChanges();
            DisplayProducts();
        }
        catch (DbUpdateConcurrencyException ex) {
            HandleConcurrencyError(ex);
        }
        catch (DbUpdateException ex) {
            HandleDatabaseError(ex);
        }
        catch (Exception ex) {
            HandleGeneralError(ex);
        }
    }
}
```

```csharp
private void DeleteProduct()
{
    DialogResult result =
        MessageBox.Show($"Delete {selectedProduct.ProductCode.Trim()}?",
        "Confirm Delete", MessageBoxButtons.YesNo, MessageBoxIcon.Question);
    if (result == DialogResult.Yes)
    {
        try
        {
            context.Products.Remove(selectedProduct);
            context.SaveChanges(true);
            DisplayProducts();
        }
        catch (DbUpdateConcurrencyException ex)
        {
            HandleConcurrencyError(ex);
        }
        catch (DbUpdateException ex)
        {
            HandleDatabaseError(ex);
        }
        catch (Exception ex)
        {
            HandleGeneralError(ex);
        }
    }
}

private void btnAdd_Click(object sender, EventArgs e)
{
    var addModifyProductForm = new frmAddModifyProduct() {
        AddProduct = true
    };
    DialogResult result = addModifyProductForm.ShowDialog();
    if (result == DialogResult.OK)
    {
        try
        {
            selectedProduct = addModifyProductForm.Product;
            context.Products.Add(selectedProduct);
            context.SaveChanges();
            DisplayProducts();
        }
        catch (DbUpdateException ex)
        {
            HandleDatabaseError(ex);
        }
        catch (Exception ex)
        {
            HandleGeneralError(ex);
        }
    }
}

private void HandleConcurrencyError(DbUpdateConcurrencyException ex) { ... }
private void HandleDatabaseError(DbUpdateException ex) { ... }
private void HandleGeneralError(Exception ex) { ... }

private void btnExit_Click(object sender, EventArgs e)
{
    this.Close();
}
```

图22-9    产品维护窗体的代码（第3部分，共3部分）

## 如何为 DataGridView 控件提供分页功能

如果 DataGridView 控件的数据源包含大量行，您可能需要让用户逐页显示这些行，而不是使用滚动条。由于应用程序一次只检索一页的数据行，这样工作效率会更高。

## 提供分页功能的窗体用户界面

图22-10 展示了使用分页功能的 Customer Display 应用程序的用户界面。这里，四个分页控件位于网格下方左侧。这些控件使用户可以移到第一页、上一页、下一页和最后一页。在本例中，显示的是第一页，因此 First 和 Previous 按钮处于禁用状态。

在大多数情况下，您还需要包含可以让用户跳转到特定页面的控件。例如，要显示姓名在字母顺序中位于中间附近的客户，用户可以在网格下方的文本框中输入中间页码，然后点击 Go To Page 按钮。如有必要，随后用户可以点击 Previous 或 Next 按钮来定位该客户。这比多次点击 Next 按钮才到达同一页要高效得多。

## 提供分页功能的 Customer Display 窗体

![](img/844f608d10a44654833ea5efc8a2e7a7_771_0.png)

## 说明

- Customer Display 应用程序用于显示 Customers 表中所有客户的数据，每页显示十位客户。为此，它使用了 Entity Framework Core 和 LINQ to Entities。
- 用户可以点击网格下方左侧的四个按钮来显示第一页、上一页、下一页或最后一页。这些按钮会根据所显示的页面被启用或禁用。
- 网格下方的文本框显示当前显示的页面，文本框右侧的标签显示总页数。用户可以在文本框中输入页码，然后点击 Go To Page 按钮来跳转到特定页面。

## 窗体的代码

图22-11 展示了使用 EF 实现分页的代码。首先，这段代码声明了一些类级变量和一个常量。名为 MaxRows 的常量表示每页可显示的最大行数。名为 totalRows 的变量存储总行数。名为 pages 的变量存储总页数。

窗体的 Load 事件处理程序首先使用 Customers 实体集合的 Count() 方法获取总行数。然后，它计算页数。为此，它将总行数除以每页的最大行数。接着，它使用取模运算符来检查除法运算后是否有剩余行。如果有，它会将页数加一。

完成这些计算后，该代码会在文本框右侧的标签中显示总页数。然后，Load 事件处理程序以调用 DisplayCustomers() 方法并向其传递值 1 来结束，以显示第一页客户数据。

DisplayCustomers() 方法首先在窗体的文本框中显示当前页码。然后，它计算名为 skip 和 take 的变量的值。skip 变量存储检索行之前要跳过的行数，take 变量存储要为特定页检索的行数。

为了计算 take 变量，代码首先将其设置为等于 MaxRows 常量。在大多数情况下，这是 take 变量的正确值，因为这样会显示一整页数据。然而，如果当前页码等于总页数，代码会将 take 变量设置为总行数减去 skip 变量。这是因为最后一页可能没有整页的数据。同样，如果总行数小于或等于每页的最大行数，该代码会将 take 变量设置为 totalRows 变量。这是因为在这种情况下，第一页不会显示整页数据。

计算出 take 变量后，该代码使用 LINQ 查询获取要显示的客户。为此，它把 skip 和 take 变量传递给 Skip() 和 Take() 方法。然后，它检索实体，将其转换为列表，并将该列表用作网格的数据源。

为网格设置数据源后，该代码会对网格进行格式化，使其显示效果与前一图所示一致。为此，它使用了图22-9 所示的产品维护应用程序所使用的相同技术。

DisplayCustomers() 方法最后将其 pageNumber 参数传递给 EnableDisableButtons() 方法。该方法会根据页码启用或禁用窗体上的按钮。
