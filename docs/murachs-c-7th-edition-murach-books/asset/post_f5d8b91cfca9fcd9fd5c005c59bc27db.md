
## The code that implements the paging

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

The EnableDisableButtons() method begins by checking whether the page number is equal to 1. If so, the application is displaying the first page of customer rows. In that case, this code disables the First and Previous buttons. Otherwise, the application is displaying a page other than the first page. In that case, this code enables the First and Previous buttons.

Then, this method checks whether the page number is equal to the total number of pages. If so, the application is displaying the last page of customer rows. In that case, this code disables the Next and Last buttons. Otherwise, the application is displaying a page other than the last page. In that case, this code enables the Next and Last buttons.

Finally, this method checks whether the total number of rows is less than or equal to the maximum number of rows for a page. If so, there’s only one page of customer rows. In that case, none of the navigations buttons on this form are necessary. However, the previous if statements have already disabled the First, Previous, Next, and Last buttons. As a result, the code for the third if statement just disables the Go To Page button.

## The code that implements the paging

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

## The code that implements the paging

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

## How to create a Master/Detail form

You can also use DataGridView controls to display data in related tables of a database. To do that, you can use one grid to display the rows on the one side of the relationship and another to display the rows on the many side of the relationship.

## The user interface for a Master/Detail form

Figure 22-12 presents the user interface for a Master/Detail form that uses two DataGridView controls. This form lets users select a customer from the Customers grid. Then, it displays the invoices for that customer in the Invoices grid.

In addition, the Customers grid provides paging controls. Then, each time a different page is displayed, the first customer on that page is selected by default and any invoices for that customer are displayed in the Invoices grid. To display the invoices for another customer on the page, the user can click on the row header for that customer. In this figure, for example, the user clicked on the row header for the customer named Sarah Chamberland. Then, the Invoices grid displayed the three invoices for that customer.

## A Master/Detail form that displays customers and invoices

![](img/844f608d10a44654833ea5efc8a2e7a7_779_0.png)

- The Customer Invoice Display application displays data about customers and their related invoices. To do that, it uses two DataGridView controls.
- Paging is provided for the DataGridView control that displays the customer data. This works the same as for the Customer Display application shown in figures 22-10 and 22-11.
- When a page of customers is first displayed, the first customer is selected and any invoices for that customer are displayed in the second DataGridView control.
- To display the invoices for another customer, the user clicks the row header for that customer.

> Figure 22-12 The user interface for a Master/Detail form

## The code for the form

Figure 22-13 shows the code that’s needed to implement the Master/Detail form. To start, the DisplayCustomers() method is mostly the same as in the Customer Display application presented earlier in this chapter.

One difference is that the DisplayCustomers() method now retrieves the customer ID in addition to the other columns. That’s because the application now needs the customer ID to get the related invoices for a customer. However, this application doesn’t display the customer ID in the grid. Instead, the code sets the Visible property of that column to false as shown in this figure.

Another difference is that the DisplayCustomers() method includes code that selects the first customer on the page and displays that customer’s invoices. To do that, it uses one statement to select the first row of the Customers grid, which has an index of 0. Then, it uses a second statement to pass a value of 0 to the DisplayInvoices() method. This displays the invoices for the first row of the Customers grid.

When the user clicks the row header for a customer, the event handler for the RowHeaderMouseClick event is executed. This event handler calls the DisplayInvoices() method and passes the RowIndex property of the DataGridViewCellMouseEventArgs parameter to it. This provides the index of the row that was clicked.

The code for the DisplayInvoices() method starts by getting the row that the user clicked. Then, it gets the value of the first cell in that row, which contains the customer ID. Next, it uses LINQ to get a list of invoices with that customer ID. Finally, it assigns the list to the DataSource property of the Invoices grid. This displays the invoices in that grid.

## The code that implements the Master/Detail form

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
