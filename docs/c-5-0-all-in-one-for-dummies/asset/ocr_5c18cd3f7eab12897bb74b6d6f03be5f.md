```
```csharp
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;

namespace Accessing_Data
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void partsBindingNavigatorSaveItem_Click(object sender, EventArgs e)
        {
            this.Validate();
            this.partsBindingSource.EndEdit();
            this.tableAdapterManager.UpdateAll(this.assets_MaintenanceDataSet);
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            // TODO: This line of code loads data into the "assets_MaintenanceDataSet.Part_Faults" table. You can move, or remove it, as needed.
            this.part_FaultsTableAdapter.Fill(this.assets_MaintenanceDataSet.Part_Faults);
            // TODO: This line of code loads data into the "assets_MaintenanceDataSet.Parts" table. You can move, or remove it, as needed.
            this.partsTableAdapter.Fill(this.assets_MaintenanceDataSet.Parts);
        }
    }
}
```
```

While this is fairly straightforward, it obviously isn’t everything that you need. The rest of the code is in the file that generates the visual form itself, supporting the visual components.

The time may come when you want to connect to a database without using visual tools. I discuss the steps in the earlier section “How the Data Classes Fit into the Framework,” and here I show the code to go with it:

+   1. `SqlConnection mainConnection = new SqlConnection();`
+   2. `mainConnection.ConnectionString = "server=local;database=assets_Maintenance;Trusted_Connection=True";`
+   3. `SqlDataAdapter partsAdapter = new SqlDataAdapter("SELECT * FROM Parts", mainConnection);`
+   4. `DataSet partsDataSet = new DataSet();`
+   5. `mainConnection.Open();`
+   6. `partsAdapter.Fill(partsDataSet);`
+   7. `mainConnection.Close();`

![](bbox=[0.153, 0.869, 0.23, 0.939])

This becomes useful especially when you want to build a web service or a class library — though it should be noted that you can still use the visual tools in those project types.