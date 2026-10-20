# The specifications
for the enhanced ProductList class

Figure 13-2 shows the specifications for an enhanced version of the ProductList class. To start, this class provides two indexers that let you access a product based on its index or product code (instead of using the GetProductByIndex() method). Besides these indexers, the enhanced ProductList class includes a + operator that adds a product to the list and a - operator that removes a product from the list.

Finally, this class includes a delegate named ChangeHandler, and an event named Changed. The delegate is designed to wire event handlers to the Changed event of the ProductList class. The ProductList class raises this event whenever the contents of the product list changes due to a product being added to, updated in, or removed from the list. As you’ll see, the Product Maintenance application uses this event to determine when it should save the product list and refresh the list box that displays the products.