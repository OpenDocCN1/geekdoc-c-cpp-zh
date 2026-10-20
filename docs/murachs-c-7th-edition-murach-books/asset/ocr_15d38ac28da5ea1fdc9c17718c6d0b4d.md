# An inheritance version
of the Product Maintenance application

Now that you’ve learned how to create base classes and subclasses, the following topics present a version of the Product Maintenance application that uses inheritance. This version of the application uses the classes that were described in figure 14-4. It works with a Products file that can hold two distinct types of products: books and software.

Note that this version of the Product Maintenance application won’t work with the ProductDB classes that are presented in chapter 17, since those classes are designed to work only with Product objects. Instead, this version of the application requires a ProductDB class that can save and retrieve data for both Book and Software objects. Although this class isn’t presented here, you shouldn’t have any trouble figuring out how to implement it after you read chapter 17.

# The operation
of the Product Maintenance application

Figure 14-8 shows the operation of this version of the Product Maintenance application. As you can see, the Product Maintenance form looks just like the one you saw in chapter 12. From this form, you can click the Add Product button to display the New Product form, or you can select a product in the list and then click the Delete Product button to delete a product.

The main difference between this application and the application presented in chapter 12 is that the New Product form includes two radio buttons. These buttons let the user choose whether a book or a software product is added to the file. Note that the label that’s displayed for the third text box changes depending on which of these buttons is selected. If the Book button is selected, this label is set to Author. If the Software button is selected, it’s set to Version.