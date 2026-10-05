
# The code for a simplified version of the Product base class

```csharp
public class Product
{
    public string Code { get; set; }
    public string Description { get; set; }
    public decimal Price { get; set; }

    public virtual string GetDisplayText(string sep)
    {
        return Code + sep + Description + sep + Price.ToString("c");
    }
}
```

# Access modifiers

| Keyword | Description |
| --- | --- |
| public | Available to all classes. |
| protected | Available only to the current class or to derived classes. |
| internal | Available only to classes in the current assembly. |
| protected internal | Available only to the current class, derived, or classes in the current assembly. |
| private | Available only to the containing class. |

# Description

- You create a base class the same way you create any other class: by defining its properties, methods, events, and other members.
- Access modifiers specify the accessibility of the members declared by a class. Public members are accessible only to the class in which they're defined.
- Protected members are accessible within the class in which they're declared. They can be used by any class that inherits the class in which they're declared.
- A derived class can access the public and protected members of its base class, but not the private members.
- Internal members are accessible by other classes in the same assembly, but not by classes in other assemblies. This can sometimes be useful to access members declared by classes in a class library. For more information about class libraries, see chapter 16.
- If you want to be able to override a member in a derived class, you must include the virtual keyword on the member declaration.
- If you don't code an access modifier, the default access is private.

# How to create a subclass

Figure 14-6 shows how to create a subclass. To indicate that a class is a subclass, you follow the class name on the class declaration with a colon: the code for the name of the base class that the subclass inherits. For example, the Book class shown in this figure specifies that the Book class is a subclass of the Product class.

After you identify the base class, you can extend its functionality by coding additional properties, methods, or other members. In this figure, for example, the Book class adds a new constructor and a new property named Author. In addition, it overrides the GetDisplayText method by the Product class.

The constructor for the Book class accepts four parameters: code, description, author, and price. A colon after followed by the base keyword and a parameter list indicates that this constructor should call the constructor from the base class using the specified parameters. In this case, the base class constructor is called using the Book class, and price parameters that were passed initializes the Code, Description, and Price properties with these values. After the base class constructor is called, the code in the Book subclass constructor is executed. This initializes the Author field with the value passed to the author parameter.

To override the GetDisplayText method, the method declaration includes the override keyword. Note that when you override a method, the override must have the same signature as the method it's overriding. In this case, the method must use a single string parameter. This parameter receives the sep's keyword used to format the Code, Description, Author, and Price properties.

Notice that this GetDisplayText method provides its own implementation. In contrast, the GetDisplayText method in the second code example builds on the implementation of this method in the Product class. To do that, it starts by calling the GetDisplayText method of the base class, which returns a formatted string that contains the Code, Description, and Price properties. Then, it adds the Author property to the end of this string.

This figure also introduces the concept of hiding. When you use the new keyword on a subclass, the member hides the corresponding base class member. As a result, the subclass doesn't inherit the original version of the member, but uses the new version instead. Hiding is similar to overriding, but can be used only with non-virtual methods or properties. Because hiding doesn't provide for polymorphism as described in the next topic, you should avoid hiding if possible. Instead, you use virtual methods and properties whenever you expect to provide a different implementation of a method or property in a subclass.

# The syntax for creating subclasses

To declare a subclass
`public class SubclassName : BaseClassName`

To create a constructor that calls a base class constructor
`public ClassName(parameterlist) : base(parameterlist)`

To call a base class method or property
`base.MethodName(parameterlist)`
`base.PropertyName`

To hide a non-virtual method or property
`public new type name`

To override a virtual method or property
`public override type name`

# The code for a Book class

```csharp
public class Book : Product {
    public string Author { get; set; } // A new property

    Book(string code, string description, String author,
        decimal price) : base(code, description, price) {
        this.Author = author; // Initializes the Author field after
        // the base class constructor is called.
    }
    public override string GetDisplayText(string sep) {
        return this.Code + sep + this.Description
            + " (" + this.Author + ")" + sep + this.Price.ToString("c");
    }
}
```

# Another way to override a method

```csharp
public override string GetDisplayText(string sep) {
    return base.GetDisplayText(sep) + " (" + this.Author + ")";
}
```

# Description

- A constructor of a derived class automatically calls the default constructor of the base class before the derived class constructor executes. If you want to, you can call a specific base constructor.
- Polymorphism is one of the most important features of object-oriented programming. As figure 14-7 shows, polymorphism lets you treat objects of different types as if they were the same type.
- One benefit of polymorphism is that you can write generic code that's designed to work with a base class. For example, the List<Product> class described in figure 14-4 accepts a Product object. Since the Book and Software classes inherit the Product class, this method is also available to those classes.
- Note that to use this type of polymorphism, you must code the virtual keyword on the base class member. Otherwise, you can't override the member in the derived classes. Then, any call to the base class member executes that member regardless of the object type.
