# SQL Server Database Programming with C#

240

| RTOSelect Project | LogInform() |

```
******
using System.Data;
using System.Data.SqlClient;
using System.Data.Linq;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;

namespace RTOSelect_Project
{
    public partial class LogInform : Form
    {
        public SQLConnection sqlConnection = null;
        public LogInform()
        {
            InitializeComponent();
            // stringString = "Server=DESKTOP-24JPUFB\\SQL2019EXPRESS;" + 
            "Initial Catalog=CSE_DEPT; + "Integrated Security=True";
            string sqlString = "Server=DESKTOP-24JPUFB\\SQL2019EXPRESS;" + 
            "Initial Catalog=CSE_DEPT" + "User ID=SMART;Password=Happy2022";
            sqlConnection = new SQLConnection(sqlString);
            try {
                sqlConnection.Open();
            } catch (Exception e) {
                MessageBox.Show("SQL Server Error");
                MessageBox.Show("Error Code = " + e.ErrorCode);
                MessageBox.Show("Error Message = " + e.Message);
            } catch (InvalidOperationException e) {
                MessageBox.Show("Invalid Message = " + e.Message);
                if (sqlConnection.State != ConnectionState.Open) {
                    MessageBox.Show("Database connection Failed");
                    Application.Exit();
                }
            }
        }
    }
}
```

FIGURE 5.69 The coding for the database connection.

# 5.15.3.1 Coding Method 1: Using the Adapter to Query Data

In this section, we discuss how to use the runtime objects to query the data from the SQL database using the DataAdapter method.
Since we need to use two methods, TableAdapter (DataAdapter) and DataReader, to perform this login process, we need to add one more button to this Form. Perform the following operations to complete this addition:

+   1. Add one new button with Name as cmdTablelogin and Text as ImageIcon into this Form.
2. Change the original login button with a new Name as cmdLoginActivity and Text as ReadLogin, respectively.
3. Adjust the size of all three buttons to make them equal in the horizontal spaces.

The modified LogInform window should match one that is shown in Figure 5.70.