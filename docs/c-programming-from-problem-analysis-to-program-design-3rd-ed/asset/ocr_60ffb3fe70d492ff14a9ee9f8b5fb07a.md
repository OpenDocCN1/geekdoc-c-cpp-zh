```
OleDbCommand dbCmd = new OleDbCommand();
 dbCmd.CommandText = sql;
 dbCmd.Connection = dbConn;

 OleDbDataAdapter memberDataAdap = new
 OleDbDataAdapter();
 memberDataAdap.SelectCommand = dbCmd;
 DataSet memberDS = new DataSet();
 //DataSet declared as protected class member.
 memberDataAdap.Fill(memberDS, "memberTable");
 // Binding is only change needed that differs
 // from the Windows application
 this.dataGrid1.DataBind();
 }
 catch (System.Exception exc)
 {
 this.lblMsg.Text = exc.Message;
 }

 protected void btnSubmit_Click(object sender,
 System.EventArgs e)
 {
 this.lblSubmit.Text = "Thanks " +
 this.txtBxFname.Text +
 "! You will be contacted...";
 if (lstBxInterests.SelectedIndex > -1)
 {
 this.lblSubmit.Text +=
 " to discuss joining" +
 " the \"" +
 this.lstBxInterests.SelectedItem.Text +
 "\" team.";
 }
 }

 protected void radioButton_CheckedChanged(object sender,
 System.EventArgs e)
 {
 if (this.radBtnFresSop.Checked)
 {
 this.lblClassif.Text = "Freshmen & Sophomores ";
 }
 else if (this.radBtnJrSr.Checked)
 {
 this.lblClassif.Text = "Junior & Seniors ";
 }
 else if (this.radBtnOther.Checked)
```