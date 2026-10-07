# Data Updating and Updating with Visual C#.

| SPUpdateDeleteProject | cmdDelete_Click(object sender, EventArgs e) |
|---|---|
| A | private void cmdDelete_Click(object sender, EventArgs e) string cmd = "dbo.BeanFactorySP";
MessageBox vButton = MessageBox.YesNo;
SqlCommand command = new SqlCommand();
DialogResult Answer;
int intDelete = 0;

Answer = MessageBox.Show("Do you want to delete this record?", "Delete", vButton);
if (Answer == System.Windows.Forms.DialogResult.Yes)
| B | sqlcommand.Connection = loginForm.Connection;
command.CommandType = Type.StoredProcedure;
command.CommandText = cmdString;
sqlcommand.Parameters.Add("@fname", SqlDbType.Char).Value = ComboName.Text;
intDelete = sqlcommand.ExecuteNonQuery();
sqlcommand.Dispose();
CurrentByteFault();
if (intDelete == 0)
MessageBox.Show("The data deleting is failed");
else
ClearFault();
ImageBox.Image = null; |

FIGURE 7.32 The modified codes for the delete click method.

The modified parts have been highlighted with the bold words. Let's see how this piece of modified codes works.

+   **A.** The content of the query string now should be equal to the stored procedure, **dbo.DeleteFactorySP**, to be built in the next section.
**B.** The CommandType of the command object should be StoredProcedure to tell the project that a stored procedure should be called to perform a data updating as the project runs.

Now we have finished all coding modifications in Visual C#. environment. Let's create our two stored procedures. There are two ways to create a stored procedure:

+   1) Create it in the Microsoft SQL Management Studio 18.
2) Create it in the Server Explorer in the Visual.NET environment.

Since we are working on Visual C#. project, we then prefer to use the second way to create our stored procedures.

#  7.5.1.2 Develop Stored Procedures with the Server Explorer Window

On the Server Explorer click on the arrow-symbol icon that is next to CSE_dept data folder to connect to our database if this database was added into the Server Explorer. Otherwise you need to right click on the Data Connections folder to add and connect to our sample database. Refer to Section 5.3.1 in Chapter 5 for the detailed information of adding and connecting to our sample database.