If the System.Drawing namespace is imported and referenced, it is not necessary to fully qualify the name. When the Form Designer generates the code to set these two properties, the statements read:

```
```csharp
this.Text = "Student Union    -    Diner by the Valley";
this.BackColor = System.Drawing.Color.Goldenrod;
```
```

Both produce the same result with this application.

The complete source listing for the application is given next. The first class, Order, was written manually. Much of the code for the second file shown, which is a partial class definition for the OrderGUI class, was created by Visual Studio Form Designer. The third file contains the event-handler methods. Code was written for each of the methods following the pseudocode developed during the design of the application.

```
```csharp
// Order.cs          Author: Doyle
// Creates an order class with
// entrée, drink, and special request
// data members. Methods to calculate
// total cost of order and set each
// data member included.

using System;
using System.Windows.Forms;
namespace Diner
{
    public class Order
    {
        public string[ ] menuEntree = new
            string[ ] {"Chicken Salad",
                "Ham and Cheese",
                "Turkey", "Vegetable Wrap",
                "Tuna Salad",
                "Avocado and Cheese",
                "Club", "Peanut Butter & Jelly",
                "Grilled Cheese", "Reuben"};

        public decimal[ ] menuEntreePrice = new
            decimal[ ] {4.50m, 5.00m, 4.75m,
                4.00m, 4.50m, 4.00m, 5.50m,
                3.75m, 3.50m, 5.00m };

        private string entree;
        private bool waterSelection;
        private string drinkSelection;
        private string specialRequest;
        private decimal entreePrice;
        private decimal drinkPrice;
```
```