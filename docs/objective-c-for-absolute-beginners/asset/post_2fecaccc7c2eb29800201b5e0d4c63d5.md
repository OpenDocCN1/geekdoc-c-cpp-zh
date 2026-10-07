
| Customer | First Name | Last Name | Address Line 1 | Address Line 2 | City | State | Zip | Phone Number | Email Address | Favorite Book Genre |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

**Figure 5–3.** The customer class

You will also notice how we have broken out the address into its different parts instead of grouping it together. We separated the Address Line 1, Address Line 2, City, State, and ZIP. This is very important and will be used in your application. Let's go back to the letter you want to send your customers of a sale in your store. You might not want to send it to all of the customers that live in different states. By separating the address, you can easily filter out those customers you do not want to include in your mail.

We have also added the attribute of Favorite Book Genre to the Customer class. We added this to show how you can keep many different types of information in each class. This field may come in handy if you have a new title coming out and you want to send an e-mail alerting customers who are especially interested in mysteries. By storing this type of information, you will be able to specifically target different portions of your customer class.

A book class is also necessary in order to create our bookstore (see Figure 5–3). We will store information about the book such as author, publisher, genre, page count, and edition number (in case there are multiple editions). The Book class will also have the price for the book.

| Author | Publisher | Genre | Year Published | Number of Pages | Edition | Price |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |

**Figure 5–4.** The book class

We also added another class called the Sale class (see Figure 5–5). This class is more abstract than the other classes we have discussed because it does not describe a tangible object. You will notice how we have added a reference to a customer and a book to the Sale class. Because the Sale class will track sales of books, we will need to know which book was sold and to which customer.

| Customer | Book | Date | Time | Amount | Payment Type |
| :--- | :--- | :--- | :--- | :--- | :--- |

**Figure 5–5.** The sale class

Now that we have planned out the properties of the classes, we will need to look at some methods that each of the classes will have.

# Planning Methods

We will not add all of the methods, but the more planning you can do at the beginning, the easier it will be for you down the line. Not all of your classes will have many methods. Some may not have any methods at.

> NOTE: When planning your methods, remember to have them focus on a specific task. The more specific the method, the more likely it is that it can be reused.

For the time being, we will not add any methods to the Book class or the Bookstore class. we will focus on our other two classes.

For the Customer class, we will add methods to list the purchase history of your client. There may be other methods that you will need to add in the future but we will add just one for now. Your completed Customer class diagram should look like Figure 5–6. You will notice the line near the bottom separates the properties from the methods.

| Customer | First Name | Last Name | Address Line 1 | Address Line 2 | City | Zip | Phone Number | Email Address | Favorite Book Genre | List Purchase History |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

**Figure 5–6.** The completed customer class

For the Sales class, we have added three methods. We added Charge Credit Card, Print Invoice, and Checkout (see Figure 5–7). For the time being, you do not need to know how to implement these methods, but you need to know that you are planning adding them to your class.

# CHAPTER 5: Object Oriented Programming with Objective-C

| Sale | Customer | Book | Date | Time | Amount | Payment Type | Charge Credit Card | Print Invoice | Checkout |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

Figure 5–7. The completed mapping out the classes and the methods you are going to

Now that you have add to them, you have the beginnings of a unified modeling language (UML) diagram.
Basically, this is a diagram used by developers to plan out their classes, properties, and methods. Starting your development process by creating such a diagram will help you significantly in the long run. An in-depth discussion of UML diagrams is beyond the scope of this book. If you would like more information about this subject, smartdraw.com has a great in-depth overview of them.

```
http://www.smartdraw.com/resources/tutorials/uml-diagrams/
```

Figure 5–8 shows the complete diagram.

| Bookstore | Customer | Name | Book | Address1 | Date | Address2 | Time | City | Amount | State | Payment Type | Zip | Charge Credit Card | Phone Number | Print Invoice | Logo | Checkout |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| Book | Customer | Author | First Name | Publisher | Last Name | Genre | Address Line 1 | Year Published | Address Line 2 | Number of Pages | City | Edition | State | Price | Zip | Phone Number | Email Address | Favorite Book Genre | List Purchase History |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

Figure 5–8. The completed UML diagram for the bookstore

# Implementing the Classes

Now that we understand the objects we are going to be creating, we need to create our first object. In order to do so, we will start with a new project.

- 1. Please launch Xcode.
- 2. From the menu bar, select File > New > Project.
- 3. In the project template selector, select Application.
- 4. In the name field, name the project Bookstore.
- 5. From the menu bar, select File > New > File.
- 6. From the popup window, select Objective-C Class.
- 7. On the next screen, select the superclass.
- 8. In the name field, name the class Customer.
- 9. Now look in your main project; you should have two files. One is Customer.h and the other is Customer.m. The .h file header file that will contain information about your class. header file will list all of the properties and methods in your class, but it not actually contain the code related to them. The .m file the implementation file, is where you will write the code for your methods.
- 10. Double-click on the Customer.h file and you will see the window shown in Figure 5-2. You will not notice it contains a lot of information currently. The first, with the double slashes (//), is all comments and is not considered part of the code. Comments allow you to tell those who might read your code what each portion of code is meant to accomplish. We will not go into more detail about the other portions of the header file, except to say that all the properties of a class need to be inside the braces {} of the @Interface portion.

# CHAPTER 5: Object Oriented Programming with Objective-C

# Implementing the Classes

Now that we understand the objects we are going to be creating, we need to create our first object. In order to do so, we will start with a new project.

- 1. Please launch Xcode.
- 2. From the menu bar, select File > New > Project.
- 3. In the project template selector, select Application.
- 4. In the name field, name the project Bookstore.
- 5. From the menu bar, select File > New > File.
- 6. From the popup window, select Objective-C Class.
- 7. On the next screen, select the superclass.
- 8. In the name field, name the class Customer.
- 9. Now look in your main project; you should have two files. One is Customer.h and the other is Customer.m. The .h file header file that will contain information about your class. header file will list all of the properties and methods in your class, but it not actually contain the code related to them. The .m file the implementation file, is where you will write the code for your methods.
- 10. Double-click on the Customer.h file and you will see the window shown in Figure 5-2. You will not notice it contains a lot of information currently. The first, with the double slashes (//), is all comments and is not considered part of the code. Comments allow you to tell those who might read your code what each portion of code is meant to accomplish.

> TIP: Properties should always start with a lowercase letter. There can be no spaces in an name.

For the first property, First Name, we will add this line to our file.

NSString* firstName;

Figure 5–13. Your empty customer class
