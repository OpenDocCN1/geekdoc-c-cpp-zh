# The Product Maintenance application

Now that you’ve learned the basic skills for creating classes, the topics that follow present a Product Maintenance application that maintains a simple file of products. As you’ll see, this application uses three user-defined classes in addition to the two form classes and the Program class that starts the program by running the first form.



Figure 12-11 describes the operation of the Product Maintenance application. As you can see, this application uses two forms. The main form displays a list of the products that are stored in a file in a list box. The user can use this form to add or delete a product.

If the user clicks the Add Product button, the New Product form is displayed as a dialog box. Then, the user can enter the data for a new product and click the Save button to add the product to the file. After the product is saved, the list box in the Product Maintenance form is refreshed so it includes the new product. The user can also click the Cancel button on the New Product form to cancel the add operation.

To delete a product, the user selects the product in the list and clicks the Delete Product button. Then, a dialog box is displayed to confirm the operation. If the operation is confirmed, the product is deleted and the list box is refreshed so it no longer includes the deleted product.

This figure also shows how the Tag properties of the three text boxes on the New Product form are set. As you’ll see in a minute, the methods of the data validation class use the Tag property of these text boxes to display meaningful error messages if the user enters incorrect data.