
# Methods of the System.Object class

| Method | Description |
| --- | --- |
| ToString() | Returns a string that contains the fully qualified name of the object's type. |
| Equals(object) | Returns true if this object refers to the same instance as the specified object. Otherwise, it returns false, even if both objects contain the same data. |
| Equals(object1, object2) | A static version of the Equals method that compares two objects to determine if they refer to the same instance. |
| ReferenceEquals(object1, object2) | A static method that determines whether two objects refer to the same instance. This method is typically not overridden, so it can be used for instance equality in classes that override the Equals method. |
| GetType() | Returns a Type that represents the type of an object. |
| GetHashCode() | Returns the integer hash code for an object. This method is called by the garbage collector when it determines that there are no more references to the object. |
| Finalize() | |
| MemberwiseClone() | Creates a shallow copy of an object. For more information, refer to chapter 15. |

# Description

- System.Object is the root base class for all classes. In other words, every class inherits System.Object or some other class that ultimately inherits System.Object. As a result, the methods defined by System.Object are available to all classes.
- When creating classes, it's a common practice to override the ToString and Equals methods so they work appropriately for each class. For example, the ToString method might return a value that uniquely identifies an object. And the Equals method might compare two objects to see if their values are equal.
- The hash code for an object is an integer that uniquely identifies the object. Given the same data, each instance of an object should return the same hash code. A common way to implement the GetHashCode method is to return ToString().GetHashCode(). This returns the hash code of the object's ToString result.
- In general, you don't need to override the Finalize method for an object, even though its default implementation doesn't do anything. That's because the .NET garbage collector automatically reclaims the memory of an object whenever it needs to. Before it does that, it calls the Finalize method of the object.

## 14-3 Methods inherited from the System.Object class

# How to use inheritance in your applications

14-4 describes the two main ways inheritance is used in business applications. First, it can be used to simplify the task of creating classes that represent similar types of objects. For example, the first inheritance hierarchy in this figure shows how you might use inheritance to create classes for two types of products: books and software products. As you can see, the Product class is used as the base class for the Book and Software classes. These subclasses inherit the Code, Description, and Price properties as well as the GetDisplayText method from the Product class. In addition, each class adds a property that's unique to the: The Book class adds an Author property,

The second inheritance hierarchy in this figure shows how you can use the classes of the .NET Framework as base classes for your own classes. Here, a ProductList class inherits the System.Collections.Generic<Product> class. That way, the ProductList class has all of the features of a List<> of Product objects (such as an indexer and a Remove method). However, the ProductList class provides its own Add method that is used instead of the Add method that's available from the List class. This lets you change any members in the base class that don't work the way you want to. You'll learn more about how this works in figure 14-6. Finally, the ProductList class provides two methods (the Fill and Save methods) that don't exist in the base class. These methods allow you to read and write the list to a data store.

An important aspect of inheritance is that you can use a subclass as an argument or return value for any method that is designed to work with the base class. For example, the Add method of the ProductList class accepts a parameter of type Product. However, because both the Book and Software classes are subclasses of the Product class, you can pass either a Book or a Software object to the Add method to add a book or software product to the product list. You'll learn more about how this works in figure 14-7.

# Chapter 14 How to work with inheritance 429

# Business classes for a Product Maintenance application

| Product |
| --- |
| string Code |
| string Description |
| decimal Price |
| string GetDisplayText(string) |

| Book |
| --- |
| string Code |
| string Description |
| decimal Price |
| string GetDisplayText(string) |
| string Author |

| Software |
| --- |
| string Code |
| string Description |
| decimal Price |
| string GetDisplayText(string) |
| string Version |

| System.Collections.Generic.List<Product> |
| --- |
| Product this[index] |
| void Add(product) |
| void Remove(product) |

| ProductList |
| --- |
| void Add(product) |
| void Fill() |
| void Save() |

# Description

- You can use inheritance in your applications to create generic base classes that implement common elements of related subclasses. For example, if you need separate classes to represent distinct types of products, you can create a Product base class, then use it to create a separate subclass for each type of product.
- It's also common to create classes that inherit from classes that are defined by the .NET Framework. For example, you might create a ProductList class that inherits the List<Product> class.
- When you inherit a class, you can use the derived class whenever the base class is called for. For example, a ProductList object based on a class that inherits List<Product> can be used whenever a List<Product> object is called for.

Figure 14-4 How to use inheritance in your applications

# Basic skills for working with inheritance

Now that you've been introduced to the basic concepts of inheritance, you're ready to see how inheritance is actually implemented in C#. In the topics that follow, you'll learn how to create both base classes and subclasses. In addition, you'll learn how to take advantage of one of the major features of inheritance, called polymorphism.

# How to create a base class

Figure 14-5 shows how to create a class that can be used as a base class for one more derived classes. To start, define the properties, methods, and other members of the class just as you would for any other class. Then, if you want a class that's derived from this class to be able to override one of the members of the base class, you include the virtual keyword on the declaration for that member. The code shown in this figure, for example, uses the virtual keyword on the GetDisplayText method. Members that specify the virtual keyword are called virtual members.

Notice that the Product class provides an implementation of the GetDisplayText method that returns a string containing the values for the Code, Description, and Price properties. If a derived class doesn't override the GetDisplayText method, it will simply inherit the version implemented by this class. As a result, creating a virtual member gives you the option of overriding the member in the derived class or allowing the derived class to defer to the version defined by the base class.

The table in this figure lists several access modifiers which indicate whether members of a base class are accessible to other classes. You already know how to use the private and public modifiers. When working with inheritance, you also need to know about the protected modifier. A protected member is a member that can be accessed within the defining class and within any class that's derived from the defining class, but not by any other class. Protected members let derived classes access certain parts of the base class without exposing those to other classes.

The internal and protected access modifiers are sometimes useful when you work with class libraries or solutions that have more than one project. To understand how they work, remember that when you build a project, all of the classes that make up the project are compiled into a single assembly. Members that use the internal keyword are accessible to all of the classes within that assembly, but not to classes in other assemblies. Similarly, members that specify protected internal are accessible to derived classes that are a part of the same assembly, but not to other assemblies.
