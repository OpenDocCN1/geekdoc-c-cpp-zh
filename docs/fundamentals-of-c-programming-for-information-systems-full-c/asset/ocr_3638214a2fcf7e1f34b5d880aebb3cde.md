```
float amtDue;
private void hsbNumOfTickets_ValueChanged(object sender, EventArgs e)
{
    lblNumOfTickets.Text = hsbNumOfTickets.Value.ToString();
}

private void btnClear_Click(object sender, EventArgs e)
{
    hsbNumOfTickets.Value = 0;
    chkMember.CheckState = CheckState.Indeterminate;
    rdbDefault.Checked = true;
    lblAmtDue.Text = "";
    cboShow.SelectedIndex = -1;
}

private void TheaterTickets_Load(object sender, EventArgs e)
{
    chkMember.CheckState = CheckState.Indeterminate;
    rdbDefault.Checked = true;
    string[] shows = { "Mamma Mia", "Rock of Ages", "Les Miserables",
        "Motown", "The Lion King", "The Phantom of the Opera" };
    foreach (string show in shows)
        cboShow.Items.Add(show);
}

private void btnComputePrice_Click(object sender, EventArgs e)
{
    // Verify that the user selected number of tickets
    if (hsbNumOfTickets.Value == 0)
    {
        MessageBox.Show("Please specify number of tickets");
        return;
    }
    // Verify that the user selected a section
    if (chkMember.CheckState == CheckState.Indeterminate)
    {
        MessageBox.Show("Please specify membership");
        return;
    }
    // Verify that the user selected membership status
    if (rdbDefault.Checked == true)
    {
        MessageBox.Show("Please specify Section");
        return;
    }
    // Get number of tickets
    int numOfTickets = hsbNumOfTickets.Value;

    // Compute discount
    float discount = Discount();

    // Get unit price
    float unitPrice = UnitPrice();

    amtDue = numOfTickets * (unitPrice - discount);
    lblAmtDue.Text = amtDue.ToString("$#,###.00");
}
```