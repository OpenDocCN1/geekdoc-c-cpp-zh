
Object-oriented development techniques work well for constructing multitier applications. As you review Figure 11-1, think of each of the components in the diagram as independent classes, separate from each other. Classes can be designed and new subclasses created that extend the functionality of the original class. Many different applications can reuse these classes through extending or combining them into new applications.

In C#, in addition to creating .EXE files, you can create class library files with a dynamic link library (DLL) extension. These files can become the components that are referenced from any number of applications. To take advantage of the features of object-oriented programming, one of the key concepts you must understand is inheritance.

## INHERITANCE

Inheritance allows you to create a general class and then define specialized classes that have access to the members of the general class. These new specialized classes can extend functionality by adding their own new unique data and behaviors. Inheritance is associated with an “is a” relationship. A specialized class “is a” form of the general class. For example, you might create a class called Person and include data characteristics of identification number, name, age, and home address. In regions that use a Social Security number for identification such as here in the United States, the Social Security number would be the identification number. Behaviors or methods titled Eat( ), Walk( ), and Talk( ) might be included. After these are defined, you could create specialized classes such as Student or Faculty that inherit from the Person class. Student “is a” Person, just as Faculty “is a” Person. Student might have unique data characteristics of student ID, major, and year in school. Through using inheritance, applications instantiating objects of the Student class would not have only the unique characteristics of the student (student ID, major, and year), but also have access to the characteristics of the Person (identification number, name, age, and address).

![](img/e33ae760e23d89eac66541252ad65de8_681_0.png)

Classes can also have a “has a” relationship in which a single class is defined to have instances of other class types. This is a concept called containment or aggregation. You experience containment in C# when you define classes that instantiate objects of the string or int classes. However, “has a” relationships are usually associated with user-defined classes. For example, a Person “has a” medicalRecord and “has a” dentalRecord.

### Inheriting from the Object Class

You have been creating your own classes since you wrote your first program in Chapter 1. You learned that every object created in C# automatically inherits from a base class named object that is in the System namespace. Object has four methods that every class written in C# inherits as long as it provides a reference to the System namespace. One of these, the ToString() method, you have used in many of your programs. Figure 11-2 uses IntelliSense to show the signature for Object.ToString() and the names of the other methods inherited from object.

![](img/e33ae760e23d89eac66541252ad65de8_682_0.png)

**Figure 11-2** Methods inherited from an object

### Inheriting from Other .NET FCL Classes

You also experienced inheritance when you developed Windows-based programs in Chapters 9 and 10. The Windows Forms classes that you created inherited from the System.Windows.Forms.Form class. Extending that class enabled you to build on the functionality that was included as part of that .NET Framework class. Adding instantiated objects from classes such as Button, Label, TextBox, and ListBox enabled you to add functionality to your program with minimal programming. To inherit from the System.Windows.Forms.Form class, new entries were added to your class definition. Figure 11-3 illustrates what Visual Studio adds when you decide to build a Windows application by choosing the Windows Application template from the Project Type menu.

![](img/e33ae760e23d89eac66541252ad65de8_682_1.png)

**Figure 11-3** Derived class

In object-oriented terminology, the class listed after the colon in Figure 11-3 is the base class. The class to the left of the colon, PresentationGUI, is called the **derived class**. To inherit from a base class, a colon is used as a separator between the derived class and the base class, as shown in Figure 11-3. PresentationGUI is the user-defined name. The Form class belongs to the System.Windows.Forms namespace. For this example, the user-defined **class** is inheriting from a predefined .NET **class**; however, the same concepts apply when a user-defined **class** is inheriting from another user-defined **class**. By using the colon, you indicate that the PresentationGUI **class** derives from the Form **class**.

### Creating Base Classes for Inheritance

You can define your own classes from which other classes can inherit characteristics. Example 11-1 creates a class named Person with four data members. This class is used as a base class from which other classes can inherit characteristics. The base class is sometimes called the **super** or **parent** class.

### Example 11-1

```csharp
public class Person
{
        private string idNumber;
        private string lastName;
        private string firstName;
        private int age;

        public Person()              // Constructor with zero arguments
        {
                idNumber = "";
                lastName = "unknown";
                firstName = string.Empty;
                age = 0;
        }
        public Person(string id, string lname, string fname,
                      int anAge)     // Constructor with four arguments
        {
                idNumber = id;
                lastName = lname;
                firstName = fname;
                age = anAge;
        }
        public Person(string id, string lname, string fname)
        {                            // Constructor with three arguments
                idNumber = id;
                lastName = lname;
                firstName = fname;
                age = 0;
        }
        public Person(string id)
        {                            // Constructor with one argument
                idNumber = id;
                lastName = "unknown";
                firstName = string.Empty;
                age = 0;
        }
}
```

Only data members and constructor methods are shown for the **Person class** in Example 11-1. Notice that the data members are defined with a private access modifier and constructors are defined with public access modifiers. The next section reviews why these choices were made.

### Access Modifiers

Access to members that have been defined with the private access modifier is restricted to members of the current class. The private members are not accessible to other classes that derive from this class or that instantiate objects of this class. Using a private access modifier enables the class to protect its data and only allow access to the data through its methods or properties. This ensures the data-hiding characteristic of encapsulation.

**Constructors Use Public Access**   Constructors, named the same name as the class name, are defined with public access. It is important to note that if you do not use a public access modifier with constructors, no objects can be instantiated from the class. Constructors differ from other methods in that they cannot have a return type. Remember that you have an **overloaded method** when you have more than one method using the same identifier. The requirement for an overloaded method is that each of the methods must have a different number and/or type of parameter from the others. Thus, by definition, when you have two or more constructors for a class, you have overloaded methods.

**Properties Offer Public Access to Data Fields**   Before creating a specialized class to inherit the characteristics of the **Person class**, properties are added to the **Person class**. By including properties, there is less need to write accessor (getter) and mutator (setter) methods. The private member fields can be accessed through these properties.

![](img/e33ae760e23d89eac66541252ad65de8_684_0.png)

Properties are new to the C/C++/C# programming family line. They look like data fields, but are implemented as methods that can be used to get or set a private data field instance.

Example 11-2 shows some of the properties added to the **Person class**. Due to space constraints, only two of the four properties are shown. The first enables the data field, firstName, to be a read-only property; it does not contain a set property. Without defining an additional mutator method, firstName can never be changed after it is constructed.
