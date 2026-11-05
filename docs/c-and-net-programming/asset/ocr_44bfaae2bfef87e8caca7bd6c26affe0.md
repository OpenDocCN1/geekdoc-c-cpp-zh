```
{ //Adding Column in table dt.Columns.Add("S_no", typeof(int)); dt.Columns.Add("S_Name", typeof(string)); dt.Columns.Add("S_Address", typeof(string)); //Adding Row in table dt.Rows.Add(1, "Aryaveer", "Ahemadabad"); dt.Rows.Add(2, "Jeetraj", "Baroda"); dt.Rows.Add(3, "Dhruvin", "Surat"); LoadRepeater(); } protected void LoadRepeater() { //Binding DataSource i.e:Datatable to a Datalist Repeater1.DataSource = dt; Repeater1.DataBind(); } protected void btnSubmit_Click(object sender, EventArgs e) { dt.Rows.Add(Convert.ToInt32(txtRoll.Text), txtName.Text,txtAddress.Text); LoadRepeater(); } }
```

# Two Marks Questions with Answers

Q.1 What is ASP.Net ?
Ans.: It is a framework developed by Microsoft on which we can develop new generation web sites using web forms(aspx), MVC, HTML, Javascript, CSS etc. Its successor of Microsoft Active Server Pages(ASP). Currently there is ASP.NET 4.0, which is used to develop web sites. There are various page extensions provided by Microsoft that are being used for web site development. Eg: aspx, asmx, ascx, ashx, cs, vb, html, XML etc.

Q.2 What is the difference between Server.Transfer and Response.Redirect ?
Ans.: In Server.Transfer page processing transfers from one page to the other page without making a round-trip back to the client's browser. This provides a faster response with a little less overhead on the server. The clients url history list or current url Server does not update in case of Server.Transfer.