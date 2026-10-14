# The code for the Shopping Cart application

Now that you’ve learned the basic skills for developing a multi-form application, you’re ready to see all the aspx and C# code for the Shopping Cart application. Because you should be able to follow it without much trouble, I’ll keep the descriptions to a minimum.

# The code for the Product class

Figure 3-16 shows the C# code for the Product class. This class represents a product that the user can order from the Shopping Cart application. It has a property for each of the columns in the Products table except CategoryID and OnHand.

# The code for the CartItem class

Figure 3-16 also shows the code for the CartItem class, which represents one item in the shopping cart. After the parameterless constructor, the next constructor for this class accepts two parameters that are used to initialize the Product and Quantity properties. These properties hold the Product object and quantity for the cart item.

In addition to the constructors and properties, the CartItem class includes two methods. The first one, AddQuantity, is used to add the quantity that’s passed to it to the cart item. This method is called when the user adds a quantity to the cart for a product that’s already in the cart. The second one, Display, returns a string that formats the data in a cart item so it can be displayed in one line of the list box on the Cart page.