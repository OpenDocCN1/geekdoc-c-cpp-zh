

## 实现分页的代码

Page 1

```
private MMABooksContext context = new MMABooksContext();
private const int MaxRows = 10;
private int totalRows = 0;
private int pages = 0;

private void frmCustDisplay_Load(object sender, EventArgs e)
{
    totalRows = context.Customers.Count();
    pages = totalRows / MaxRows;
    if (totalRows % MaxRows != 0)
    {
        pages += 1;
    }
    lblPages.Text = " / " + pages;
    DisplayCustomers(1);
}

private void DisplayCustomers(int pageNumber)
{
    txtPage.Text = pageNumber.ToString();
    int skip = MaxRows * (pageNumber - 1);
    int take = MaxRows;
    if (pageNumber == pages)
    {
        take = totalRows - skip;
    }
    if (totalRows <= MaxRows)
    {
        take = totalRows;
    }
    var customers = context.Customers
        .OrderBy(c => c.Name)
        .Select(c => new { c.Name, c.Address, c.City, c.State, c.ZipCode })
        .Skip(skip)
        .Take(take)
        .ToList();
    dgvCustomers.DataSource = customers;
    // Code that formats the DataGridView control goes here
    EnableDisableButtons(pageNumber);
}
```

EnableDisableButtons() 方法首先检查页码是否等于 1。如果是，则应用程序正在显示客户行的第一页。在这种情况下，此代码会禁用 First 和 Previous 按钮。否则，应用程序正在显示除第一页之外的页面。在这种情况下，此代码会启用 First 和 Previous 按钮。

然后，此方法检查页码是否等于总页数。如果是，则应用程序正在显示客户行的最后一页。在这种情况下，此代码会禁用 Next 和 Last 按钮。否则，应用程序正在显示除最后一页之外的页面。在这种情况下，此代码会启用 Next 和 Last 按钮。

最后，此方法检查总行数是否小于或等于每页的最大行数。如果是，则只有一页客户行。在这种情况下，此表单上的导航按钮都不必要了。然而，之前的 if 语句已经禁用了 First、Previous、Next 和 Last 按钮。因此，第三个 if 语句的代码只是禁用 Go To Page 按钮。

## 实现分页的代码

```
private void EnableDisableButtons(int pageNumber)
{
    if (pageNumber == 1)
    {
        btnFirst.Enabled = false;
        btnPrev.Enabled = false;
    }
    else
    {
        btnFirst.Enabled = true;
        btnPrev.Enabled = true;
    }

    if (pageNumber == pages)
    {
        btnNext.Enabled = false;
        btnLast.Enabled = false;
    }
    else
    {
        btnNext.Enabled = true;
        btnLast.Enabled = true;
    }

    // if there's only one page, disable the Go To button
    if (totalRows <= MaxRows)
    {
        btnGoTo.Enabled = false;
    }
}
```

## 实现分页的代码

```
private void btnFirst_Click(object sender, EventArgs e)
{
    DisplayCustomers(1);
}

private void btnPrev_Click(object sender, EventArgs e)
{
    int pageNumber = Convert.ToInt32(txtPage.Text);
    pageNumber -= 1;
    DisplayCustomers(pageNumber);
}

private void btnNext_Click(object sender, EventArgs e)
{
    int pageNumber = Convert.ToInt32(txtPage.Text);
    pageNumber += 1;
    DisplayCustomers(pageNumber);
}

private void btnLast_Click(object sender, EventArgs e)
{
    DisplayCustomers(pages);
}

private void btnGoTo_Click(object sender, EventArgs e)
{
    if (IsValidData())
    {
        int pageNumber = Convert.ToInt32(txtPage.Text);
        DisplayCustomers(pageNumber);
    }
}
```

## 如何创建主/从表单

您也可以使用 DataGridView 控件在数据库的相关表中显示数据。为此，您可以使用一个网格显示关系一侧的行，另一个网格显示关系多侧的行。

## 主/从表单的用户界面

图 22-12 展示了使用两个 DataGridView 控件的主/从表单的用户界面。此表单允许用户从 Customers 网格中选择一个客户。然后，它在 Invoices 网格中显示该客户的发票。

此外，Customers 网格提供了分页控件。然后，每次显示不同页面时，该页上的第一个客户会被默认选中，并且该客户的任何发票都会在 Invoices 网格中显示。要显示该页面上另一个客户的发票，用户可以单击该客户的行标题。例如，在此图中，用户单击了名为 Sarah Chamberland 的客户的行标题。然后，Invoices 网格显示了该客户的三个发票。

## 显示客户和发票的主/从表单

![](img/844f608d10a44654833ea5efc8a2e7a7_779_0.png)

- Customer Invoice Display 应用程序显示客户及其相关发票的数据。为此，它使用了两个 DataGridView 控件。
- 为显示客户数据的 DataGridView 控件提供了分页功能。这与图 22-10 和 22-11 中所示的 Customer Display 应用程序的工作方式相同。
- 当客户页面首次显示时，第一个客户会被选中，并且该客户的任何发票都会在第二个 DataGridView 控件中显示。
- 要显示另一个客户的发票，用户单击该客户的行标题。

> 图 22-12 主/从表单的用户界面

## 表单的代码

图 22-13 显示了实现主/从表单所需的代码。首先，DisplayCustomers() 方法与本章前面介绍的 Customer Display 应用程序中的方法基本相同。

一个区别是 DisplayCustomers() 方法现在除了其他列之外还检索客户 ID。这是因为应用程序现在需要客户 ID 来获取客户的相关发票。然而，此应用程序不会在网格中显示客户 ID。相反，代码将该列的 Visible 属性设置为 false，如图所示。

另一个区别是 DisplayCustomers() 方法包含选择页面上第一个客户并显示其发票的代码。为此，它使用一条语句选择 Customers 网格的第一行，其索引为 0。然后，它使用第二条语句将值 0 传递给 DisplayInvoices() 方法。这会显示 Customers 网格第一行的发票。

当用户单击客户的行标题时，RowHeaderMouseClick 事件的处理程序会被执行。此事件处理程序调用 DisplayInvoices() 方法并将 DataGridViewCellMouseEventArgs 参数的 RowIndex 属性传递给它。这提供了被单击行的索引。

DisplayInvoices() 方法的代码首先获取用户单击的行。然后，它获取该行中第一个单元格的值，其中包含客户 ID。接下来，它使用 LINQ 获取具有该客户 ID 的发票列表。最后，它将列表分配给 Invoices 网格的 DataSource 属性。这会在该网格中显示发票。

## 实现主/从表单的代码

```
private void DisplayCustomers(int pageNumber)
{
    ...
    var customers = context.Customers
        .OrderBy(c => c.Name)
        .Select(c => new { c.CustomerId, c.Name, c.Address, c.City, c.State, c.ZipCode })
        .Skip(skip)
        .Take(take)
        .ToList();
    dgvCustomers.DataSource = customers;

    // select the first row of the page and display its invoices
    dgvCustomers.Rows[0].Selected = true;
    DisplayInvoices(0);

    // format customer grid
    ...
    dgvCustomers.Columns[0].Visible = false;  // hide id column
    ...
}

...

private void dgvCustomers_RowHeaderMouseClick(object sender, DataGridViewCellMouseEventArgs e)
{
    DisplayInvoices(e.RowIndex);
}

private void DisplayInvoices(int rowIndex)
{
    DataGridViewRow row = dgvCustomers.Rows[rowIndex];

    int customerID = Convert.ToInt32(row.Cells[0].Value);

    var invoices = context.Invoices
        .Where(i => i.CustomerId == customerID)
        .OrderBy(i => i.InvoiceId)
        .Select(i => new { i.InvoiceId, i.InvoiceDate, i.ProductTotal, i.SalesTax, i.Shipping, i.InvoiceTotal })
        .ToList();

    dgvInvoices.DataSource = invoices;

    // format the invoices grid
}
```

