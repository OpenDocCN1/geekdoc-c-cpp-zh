```
}
}
}
```

In Listing 4.18, all the class members are accessible, except the private members. Private members are accessible only in the class where they are declared. To implement encapsulation in the MyClass class, the private keyword is used to declare the data members, namely, x, y, and z.

Press the F5 key to run the EncapsulationExample application.

The output of the application appears, as shown in Fig.C#4.16:

![](bbox=[0.28, 0.36, 0.7, 0.44])

Fig.C#4.16

Next, let's discuss about inheritance in C#.

# Implementing Inheritance

The most important reason for using OOP in .NET applications is to promote the reusability of code and eliminate redundancy of code. To ensure reusability, the OOP languages promote the use of inheritance. Inheritance is defined as the property through which a child class obtains all the features defined in its parent class. A parent class is at a higher level in the class hierarchy as compared to the child class. For example, if we consider the parrot class as a child class, then it obtains its features from the parent class, that is, the bird class.

When a class inherits the common properties of another class, the class inheriting the properties is called a derived class and the class that allows inheritance of its common properties is called a base class. Inheritance in OOP is of four types:

+   - Single inheritance: Refers to the type of inheritance in which there is one base class and one derived class
+   - Hierarchical inheritance: Refers to the type of inheritance in which a base class is inherited by multiple derived classes
+   - Multilevel inheritance: Refers to the type of inheritance in which a class derives from a class, which is derived from some other class
+   - Multiple inheritance: Refers to the type of inheritance in which a derived class inherits more than one base class

C# supports single, hierarchical, and multilevel inheritances. In C#, you cannot implement multiple inheritance by directly inheriting from more than one base class in a single derived class, instead you use interfaces.

# Note

> Interface is a collection of data members and member functions. You learn about interface in detail later in the chapter.

Inheritance represents a kind of relationship between two classes in C#. Let's understand it through an example. Suppose there are two classes named as Class A and Class B, and the Class B is derived from the Class A, as shown in Fig.C#4.17:

![](bbox=[0.35, 0.00113, 0.65, 0.00122])

Fig.C#4.17