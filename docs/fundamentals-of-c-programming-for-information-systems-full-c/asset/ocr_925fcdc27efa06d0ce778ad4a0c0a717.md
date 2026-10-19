```
private void DisplayCurrentRow()
{
    // store the current row of the data table in a DataRowView
    int currentRow = bsEmployee.Position;
    DataRowView drvEmployee = (DataRowView) bsEmployee[currentRow];

    // copy data from the DataRowView to controls on the form:
    txtEmpId.Text = drvEmployee["EmpId"].ToString();
    // Or, use the index as in, drvEmployee[0].ToString();
    txtFirstName.Text = drvEmployee["FirstName"].ToString();
    txtLastName.Text = drvEmployee["LastName"].ToString();
    txtDOB.Text = drvEmployee["DateofBirth"].ToString();
    txtPhone.Text = drvEmployee["Phone"].ToString();
    txtCountryId.Text = drvEmployee["CountryId"].ToString();
    txtDepNo.Text = drvEmployee["DeptNo"].ToString();
    txtSalary.Text = drvEmployee["Salary"].ToString();
    chkFullTime.Checked = bool.Parse(drvEmployee["FullTime"].ToString());
    txtPosition.Text = drvEmployee["Position"].ToString();
}
private void btnFirst_Click(object sender, EventArgs e)
{
    bsEmployee.MoveFirst();
}
private void btnLast_Click(object sender, EventArgs e)
{
    bsEmployee.MoveLast();
}
private void btnPrevious_Click(object sender, EventArgs e)
{
    bsEmployee.MovePrevious();
}
private void btnNext_Click(object sender, EventArgs e)
{
    bsEmployee.MoveNext();
}
private void bsEmployee_PositionChanged(object sender, System.EventArgs e)
{
    // display data & row number whenever a the current record position changes
    if (bsEmployee.Count > 0)
    {
        DisplayCurrentRow();
        lblRecordNo.Text = (bsEmployee.Position + 1) + " of " + bsEmployee.Count;
    }
}
```

# Review Questions

12.11 To create a table adapter object using code, you need to specify the _____ and _____.

12.12 What are the benefits of creating data access objects (data adapter, data table and binding source) using code at runtime, rather than at design time using the wizard?

12.13 How does an untyped data table differ from a typed data table?