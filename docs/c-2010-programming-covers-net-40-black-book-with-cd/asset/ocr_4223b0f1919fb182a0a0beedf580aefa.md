```
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Data.Sql;
using System.Data.SqlClient;
namespace ParameterizedQueries
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        private void button1_Click(object sender, EventArgs e)
        {
            SqlDataReader rdr = null;
            SqlConnection con = new SqlConnection("Data Source=.;Initial Catalog=Northwind;Integrated Security=True");
            con.Open();
            string CommandText = "SELECT FirstName, LastName" + " FROM Employees" + " WHERE (LastName like @Find)";
            SqlCommand cmd = new SqlCommand(CommandText);
            cmd.Connection = con;
            cmd.Parameters.Add(new SqlParameter("@Find", System.Data.SqlDbType.NVarChar, 20, "LastName"));
            cmd.Parameters["@Find"].Value = textBox1.Text;
            rdr = cmd.ExecuteReader();
            listBox1.Items.Clear();
            while (rdr.Read())
            {
                listBox1.Items.Add(rdr["FirstName"].ToString() + " " + rdr["LastName"].ToString());
            }
        }
    }
}
```

Now, run the ParameterizedQueries application by pressing the F5 key. The output of the ParameterizedQueries application is shown in Figure 25.17:

![](bbox=[0.35, 0.68, 0.62, 0.88])

# Figure 25.17: Displaying Data in the ListBox Control

In Figure 25.17, as you type the last name of the employee in the Find text box and click the Click to Find button, the complete name of the employee is retrieved from the Employees table and displayed in the provided list box.