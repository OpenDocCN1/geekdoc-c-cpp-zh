```
private void fillByToolStripButton_Click(object sender, EventArgs e)
{
    try
    {
        this.table1TableAdapter.FillBy(this.dBDataSet.Table1);
    }
    catch (System.Exception ex)
    {
        System.Windows.Forms.MessageBox.Show(ex.Message);
    }
    try
    {
        this.table2TableAdapter.FillBy(this.dBDataSet1.Table2);
    }
    catch (System.Exception ex)
    {
        System.Windows.Forms.MessageBox.Show(ex.Message);
    }
}
private void button3_Click(object sender, EventArgs e)
{
    string connection = "Provider=Microsoft.Jet.OLEDB.4.0;Data Source=D:\\Minor App\\Project Planner\\DB.mdb";
    string query = "SELECT * FROM Table1";
    OleDbDataAdapter DA = new OleDbDataAdapter(query, connection);
    OleDbCommandBuilder CMD = new OleDbCommandBuilder(DA);
    DA.Fill(dBDataSet.Table1);

    BindingSource BindSource = new BindingSource();
    BindSource.DataSource = this.dBDataSet.Table1;
    this.dataGridView1.DataSource = BindSource;
    this.dataGridView1.Visible = true;
}
private void dataGridView1_CellContentClick(object sender, DataGridViewCellEventArgs e)
{
}
private void tabPage2_Click(object sender, EventArgs e)
{
}
private void label11_Click(object sender, EventArgs e)
{
}
private void button5_Click(object sender, EventArgs e)
{
    this.button6.Visible = true;
    this.label8.Visible = true;
    this.label9.Visible = true;
    this.label10.Visible = true;
    this.label11.Visible = true;
```