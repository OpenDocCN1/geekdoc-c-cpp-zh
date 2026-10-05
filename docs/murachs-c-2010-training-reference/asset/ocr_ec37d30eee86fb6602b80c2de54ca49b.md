# An enhanced version of the Product Maintenance application

created from the Product class with identical values. Then, the products are compared in an if statement using the == operator. Because both products have the Code, Description, and Price values, this comparison returns true. If the Product class didn't override the == operator, however, this comparison would return false because the p1 and p2 variables refer to different instances of the Product class, even though they have the same values.

Before I go on, you might want to consider why it's necessary for the == operator to be static. If it weren't, you would have to call it from an instance of the Product class, for example, p1. But what if p1 was null? In other words, what if p1 didn't refer to an instance of the Product class? In that case, you couldn't use the == operator. With null operands, then, overloaded operators must be declared as static.

Now that you've learned the techniques for enhancing your classes, the topics that follow present an enhanced version of the Product Maintenance application that uses those enhancements. From the user's standpoint, the application operates like the one that was presented in chapter 12. The only difference is that the classes in this version of the application are implemented differently. Specifically, the ProductList class includes the additional members that are shown in figure 13-2.

Because the code for the Product class is the same as the Product class presented in chapter 12, I won't repeat it here. Similarly, the New Product form that's used in this version of the Product Maintenance application is identical to the code shown in chapter 12. As a result, I won't repeat that code either. Finally, like the application in chapter 12, you should know that this application will work with any of the three versions of the ProductDB class that are presented in 21 and 22.

# The code for the ProductList class

Figure 13-10 shows the code for the ProductList class, which stores a collection of Product objects. To help you follow it, I've highlighted some of the critical statements.

As you can see, this class begins by declaring a List<object> named products. This instance variable is used to store the product list. Next, the ProductList declares a delegate EventHandler and an event named Changed that uses this delegate. This event is raised whenever the contents of the products list are changed.

The two indexers for this class let users of the class to access a specific product in the list by specifying an integer value or a product code. Since these indexers are similar to the two indexers in figure 13-3, you shouldn't have any