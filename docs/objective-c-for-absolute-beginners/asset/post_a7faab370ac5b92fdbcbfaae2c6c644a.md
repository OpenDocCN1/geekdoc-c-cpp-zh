
# CHAPTER 5: Object Oriented Programming with Objective-C

![](img/322e107ddf8f5cd963a6efafdcd86f38_106_0.png)

Figure 5-14. The customer class interface with properties

Now that the @interface portion is complete, we will need to add our method. Methods need to go outside of the @interface portion but still inside of the @interface portion of the header file. We will add a new method that returns an NSArray. This code will look as follows:

-(NSArray*) listPurchaseHistory;`

> NOTE: NSString is a class that holds and performs actions on a string. A string is a set of characters. NSString can hold letters, numbers, and punctuation.

That is all that needs to be done in the header file to create our class. Figure 5–15 shows the final header file. In the next chapter, we will go more detail about the implementation file.

![](img/322e107ddf8f5cd963a6efafdcd86f38_107_0.png)

Figure 5-15. The finished customer class header file

# Inheritance

Another major quality of OOP is inheritance. Inheritance in programming is similar to genetic inheritance. You might have inherited your eye color from your mother or hair color from your father, or vice versa. Classes can, in a similar way, inherit properties and methods from their parent class. In OOP, a parent class is called a superclass and a child class is called a subclass.

In Objective-C, all classes created by a programmer have a superclass that is similar to a parent class. The class will inherit characteristics from that parent class. So, just as in all other OOP languages, the class is a subclass of the parent class. In Objective-C, most of the time, your classes are subclasses of NSObject. In our previous example, the Customer class was a subclass of NSObject.

We could, for example, create a class of printed materials and use subclasses for books, magazines, and newspapers. Printed materials have many things in common, so we could assign variables to the superclass of printed materials and not have to redundantly add them to each class. By doing this, we further reduce the amount of code that is necessary for you to write and debug.

In Figure 5-16, we will see the layout for properties of Printed Material superclass and how that will affect subclasses of Book, Magazine, and Newspaper. The properties of Printed Material class will be inherited by subclasses so there is no need to define them explicitly.

| Printed Material | Properties |
| :--- | :--- |
| Book | Author |
| Magazine | Edition |
| Newspaper | Title |
| | Page Count |
| | Price |
| | Publisher |
| | Issue |

Figure 5-16

# Why Use OOP?

Throughout this chapter, we have discussed what OOP is and we have discussed how to create classes and objects. However, it is important to discuss why you want to use OOP. If you take a look at popular programming languages like Objective-C, C++, Swift, and Java, all require you to understand classes and objects successfully. Any development you do today will require you to understand object-oriented principles.

# Eliminate Redundant Code

By using objects, you can reduce the amount of code you have to write. If you write code to print a receipt in one class, you will not have to rewrite this code again. This not only saves time but often will help you eliminate mistakes. If you do not use OOP, you run the risk of having interfaces behave differently, even something as simple as a change.

# Ease of Debugging

By having all of the code relating to a book in one class, you know where to look when there is a problem. This may not sound like a big deal for a little application, but when your application gets to hundreds of thousands or even millions of lines of code, it will save you a lot of time.

# Ease of Replacement

If you place all of your code in a class, then as things change in your application, you can give your new class completely different functionality while it interacts with the rest of the application in the same way. This is similar to parts; if you want to replace an item, you do not need to start over. If you have code scattered all over the place, it makes it much more difficult to change items.

# Advanced Topics

We have discussed the basics of OOP throughout this chapter, but there are other topics that are very important to your understanding.

# Interface

As we have discussed in this chapter, the way other objects interact with each other is with methods. We discussed the header files created when you create a class. This is often called the interface because it tells other objects how they can interact with your objects. Implementing a standard interface throughout your application will allow your code to interact with different objects in similar ways. This will significantly reduce the amount of object-specific code you need to write.

# Polymorphism

Polymorphism is the ability of an object of one class to appear and be an object of another class. This is usually done by creating methods and properties that are similar to those of another class. A great example of polymorphism we have been using is the bookstore. In the bookstore, we have three classes: Book, Magazine, and Newspaper. If we wanted a big sale for our entire inventory, we could go through all of the books and mark them down, then we could go through all of the magazines and mark them down. That would be more work than we would need to do. It would be better to make sure all of the classes have a markdown method. We could call that on all of the objects needing which class they were, as long as they are subclasses of a class that contained the methods needed. This would save a bunch of time and coding.

As you are planning out your classes, look for similarities and methods that might apply to more than one type of class. This will save you time and speed up your application in the long run.

# Summary

We've finally reached the end of the chapter! Here is a summary of the things that were covered.

- Object-oriented programming (OOP)
  - We discussed the importance of OOP and the reasons why all modern code should use this methodology.
- Object
  - You learned about objects and how they correspond to real-world objects. We learned that many programming objects relate directly to real-world objects. You also learned about abstract objects that do not correspond to real-world objects.
- Class
  - You learned that a class determines the types of data (properties) and the methods that each object will have. Every object needs to have a class. It is the blueprint for the object.
- Creating a class
  - You learned how to map out the properties and methods of our classes.
  - We used Xcode to create a class file.
  - We edited the header file to add our properties and methods.
