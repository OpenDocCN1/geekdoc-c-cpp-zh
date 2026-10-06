
# Understanding this Reference

When you create a class, only one copy of the class code is stored in computer memory. However, you might eventually create thousands of objects from the class. When you create each object, you provide storage for each of the object's instance variables. For example, Figure 9-17 shows part of a Book that contains three fields, a property for the title field, and an advertising message method. When you declare several Book objects, in the following statements, each Book object requires memory locations for its title, numPages, and price:

Book myBook = new Book();
Book yourBook = new Book();

```csharp
class Book
{
    private string title;
    private int numPages;
    private double price;
    public string Title
    {
        return title;
    }
    set{
        title = value;
    }
    public void AdvertisingMessage(){
        WriteLine("Buy it now: {0}", Title);
    }
}
```

**Figure 9-17** Partially developed Book class

When you compile the Book class, you receive warnings that the numPages and price fields are never used. The omission was purposeful for this demonstration program.

In this example, storing a single Book object requires allocating storage space for three separate fields; the storage requirements for Book objects used by a library or retail bookstore would be far more considerable, but necessary—each Book must be able to "hold" its own data, including publisher, date published, author, ISBN, and so. Each nonstatic field is called an instance variable precisely because separate values are stored for each instance. In addition to its,

# CHAPTER 9 Using Classes and Objects

if each Book object required its own copy of property and method contained in the class, the storage requirements would multiply. It makes sense that each Book needs space to store its unique title and other data, but every Book uses the same methods, storing multiple copies of methods is wasteful and unnecessary.

Fortunately each Book object does not need to store its own copy of property and method. Whether you call the method myBook.AdvertisingMessage() or yourBook. AdvertisingMessage(), you access the same AdvertisingMessage() method. However, there must be a difference between the two methods, because each displays a different title in the message. The difference lies in an implicit, or invisible, reference that is this reference, which is the address of the invoking object. When you call the method myBook.AdvertisingMessage(), you automatically pass this reference to the method so that it knows which instance of Book to use. Using nonstatic methods receive this reference. The reference is aptly named. When you execute a static method as myBook.AdvertisingMessage(), you may ask yourself which object's data will be used in the method. The answer is “This object's myBook”.

You can refer to this reference within an instance method or property, as shown in Figure 9-18. When you refer to Title (or title) within a Book method or accessor, you are referring to the field of “Book—the Book whose name you used in the method call, perhaps myBook or yourBook. Using the shaded keywords in Figure 9-18 is not required; the version of the methods shown in Figure 9-17 (where this was implied but not written) works just as well. Figure 9-19 shows an application that uses the Book class, and Figure 9-20 shows the output.

```csharp
class Book {
    private string title;
    private int numPages;
    private double price;
    public string Title {
        get {
            return this.title;
        }
        set {
            this.title = value;
        }
    }
    public void AdvertisingMessage() {
        WriteLine("Buy it now: {0}", this.title);
    }
}
```

**Figure 9-18** The Book class with methods explicitly using this references

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN 02-200-022

```csharp
using System.Console;
class CreateTwoBooks
{
    static void Main()
    {
        Book myBook = new Book();
        Book yourBook = new Book();
        myBook.Title = "Silas Marner";
        yourBook.Title = "The Time Traveler's Wife";
        myBook.AdvertisingMessage();
        yourBook.AdvertisingMessage();
    }
}
```

Figure 9-19 Program declares two Book objects

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_403_0.png)

Figure 9-20 Output of the CreateTwoBooks program

The Book class in Figure 9-8 worked without adding the explicit references to this. However, you should be aware that the this reference is always there, working behind the scenes, even if you do not code it. Sometimes, you might want to include this reference within a method for clarity, the reader has no doubt when you are referring to an instance variable.

On occasion, you might need to explicitly code the this reference. For example, consider the abbreviated Book class in Figure 9-21. The programmer has chosen the identifier for a field and a parameter to a method that uses the two, the field must be referenced as this.price within the method that has a parameter with the same name. All references to price (without using this) in the SetPriceAndTax() method in Figure 9-21 are references to the local parameter. If the method included the statement price = price; the parameter's value would be assigned to itself and the class's field would never be set.

# CHAPTER 9 Using Classes and Objects

```csharp
class Book {
    private double tax;
    private double price;
    public void setPriceAndTax(double price) {
        const double TAX_RATE = 0.07;
        this.price = price;
        tax = price * TAX_RATE;
    }
}
```

Figure 9-21 Book class that must explicitly use the Reference.

Watch the video Understanding this Reference.

# TWO TRUTHS & A LIE

# Understanding this Reference

- 1. An implicit, or invisible, this reference is passed to every instance method and property accessor in a class; instance methods and properties are nonstatic.
- 2. You can explicitly refer to this reference within an instance method or property.
- 3. Although this reference exists in every instance method, it is invisible, you can never refer to it without a method.

> The reference is this
The false statement is #3. Sometimes, you might want to include this reference within a method for clarity, so the reader has no doubt when you are referring to an instance variable.

# Understanding Constructors

When you create a class such as Employee and instantiate an object with a statement such as Employee worker = new Employee(); you are actually calling a method named Employee() that is provided by C#. A constructor is a method that instantiates (creates an instance of) object. If you do not write a constructor for a class, then each class you create is automatically supplied with a public constructor with no parameters. A constructor without

parameters is a class's default constructor. (The term default constructor is not just used for a class's automatically supplied constructor; it is used for any constructor that takes no parameters. You will learn to create constructors with parameters in the next section.)

The automatically created constructor named Employee() establishes the same identifier worker, and provides the following initial values to the Employee's data fields:

- Numeric fields are set to 0 (zero).
- Character fields are set to 'w'.
- Boolean fields are set to false.
- References, as string or any other object fields, are set to null (or empty).

The value of an object initialized with a default constructor is known as the default value of the object. If you do not want all of an Employee's fields to hold default values, or if you want to perform additional tasks when you create an automatically supplied version. You must write your own constructor with the same name as its class, and constructors cannot have a return type. For example, if you create an Employee class that contains a Salary property, and you want every new Employee object to have a salary of 300.00, you could write the constructor for the Employee class as follows:

```csharp
Employee()
```

```csharp
Salary = 300.00;
```

}

Assuming a Salary property has been defined for the salary field, instantiated Employee will have a salary value of 300.00.

You can write any statement in a constructor. For example, you can perform arithmetic or display a message. However, the most common constructor task is to initialize fields. If you create a class in which one or more fields are never assigned a value, the compiler will issue a warning that the fields in question will hold default values.

# Passing Parameters to Constructors

You can create a constructor to ensure that all objects of a class are initialized with the same values in their data fields. Alternatively, you might create objects initialized with unique field by writing constructors to which you pass one or more parameters. You can use the parameter values to set properties or fields for individual object instantiations.

For example, consider an Employee class with two data fields, a constructor, and auto-implemented property, as shown in Figure 9-22. Its constructor assigns 9.99 to each instantiated Employee's PayRate. Any new Employee object is created using a statement such as Employee partTimeWorker = new Employee(); even if no other data-assigning methods are ever used, you are ensured that the Employee's PayRate holds a default value.
