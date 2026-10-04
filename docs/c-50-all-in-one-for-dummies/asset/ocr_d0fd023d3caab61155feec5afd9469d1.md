# 432 Using the System.DataNamespace

```
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;

namespace Accessing_Data
{
    public partial class Forml : Form
{
        public Forml()
        {
            InitializeComponent();
        }

        private void voidBindingNavigatorSaveItem_Click(object sender, EventArgs e)
        {
            this.Validate();
            this.partsBindingSource.EndEdit();
            this.tableDataAdapter.UpdateAll(this.MaintenanceDataSet);
        }

        private void voidLoad(object sender, EventArgs e)
        {
            // TODO: This line of code loads data into the 'assets_
            MaintenanceDataSet.Part_Faults' table. You can move, or remove it, as needed.
            this.part_FaultsTableAdapter.Fill(this.assets_MaintenanceDataSet);

            // TODO: This line of code loads data into the 'assets_
            MaintenanceDataSet.Parts' table. You can move, or remove it, as needed.
            this.partsTableAdapter.Fill(this.assets_MaintenanceDataSet);
        }
    }
}
```

While this is fairly straightforward, it obviously isn't everything that you need. The need for the code is in the function that generates the visual form itself, supporting the visual components.

The time may come when you want to connect to a database without using visual tools. I discuss the steps in the first section "How Data Classes Fit into the Framework," and here I show the code to go with it:

> This becomes especially useful when you want to build a web service or a class library — though it should be noted that you can still use the visual tools in those projects.

![](bbox=[0.145, 0.88, 0.225, 0.945])