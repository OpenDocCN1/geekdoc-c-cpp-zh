# The code that implements the paging

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