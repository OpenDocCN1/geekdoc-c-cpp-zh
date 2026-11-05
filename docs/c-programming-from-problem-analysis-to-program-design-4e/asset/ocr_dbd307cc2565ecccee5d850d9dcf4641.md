```
```csharp
{
    public partial class OrderGUI : Form
    {
        public OrderGUI( )
        {
            InitializeComponent( );
        }

        // Instantiates an object of the Order class when
the form is first loaded.
        private void OrderGUI_Load(object sender,
                                   System.EventArgs e)
        {
            newOrder = new Order( );
            for(int i = 0; i < newOrder.menuEntree.Length; i++)
            {
                this.lstBxEntree.Items.Add
                    (newOrder.menuEntree[i]);
            }
        }

        // Event handler that gets the entree from the
        // ListBox and sets the entree price.
        private void lstBxEntree_SelectedIndexChanged
            (object sender, System.EventArgs e)
        {
            newOrder.Entree = this.lstBxEntree.Text;
        }

        // Event handler that gets the special request -
        // if one is selected from the predefined list.
        private void cmbSpecial_SelectedIndexChanged
            (object sender, System.EventArgs e)
        {
            newOrder.SpecialRequest =
                this.cmbSpecial.Text;
        }

        // Menu item that displays the order
        private void menuDisplayOrder_Click(object sender,
                                            System.EventArgs e)
        {
            MessageBox.Show
                (newOrder.Entree + "\n"
                    + newOrder.SpecialRequest
                    + "\n"
                    + newOrder.DrinkSelection
                    + "\n" +
                    newOrder.GetWaterSelection( ),
                    "Current Order");
        }
    }
}
```
```