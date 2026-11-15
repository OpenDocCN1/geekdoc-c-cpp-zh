
types. This is the core construct of any C# program, and the complete support for classes and the objects created from them is what defines C# as an object-oriented language.

This chapter introduces you to the basics of object-oriented programming using C#. A key focus is on how to define classes, which are the templates for objects themselves.

All of the constructs of structured programming from the previous chapters still apply within object-oriented programming. However, by wrapping those constructs within classes, you can create larger, more organized programs that are more maintainable. The transition from structured, control-flow-based programs to object-oriented programs somewhat revolutionized programming because it provided an extra level of organization. The result was that smaller programs were simplified somewhat; but more importantly, it was possible to create much larger programs because the code within those programs was better organized.

One of the key advantages of object-oriented programming is that instead of creating new programs entirely from scratch, you can assemble a collection of existing objects from prior work, extending the classes with new features, adding more classes, and then reassembling everything to provide new functionality.

Readers unfamiliar with object-oriented programming should read the Beginner Topic blocks for an introduction. The general text outside the Beginner Topics focuses on using C# for object-oriented programming with the assumption that readers are already familiar with object-oriented methodology.

This chapter delves into how C# supports encapsulation through its support of constructs such as classes, properties, and access modifiers (we covered methods in the preceding chapter). The next chapter builds on this foundation with the introduction of inheritance and the polymorphism that object-oriented programming enables.

### BEGINNER TOPIC
### Object-Oriented Programming

The key to programming successfully today is in the ability to provide organization and structure to the implementation of complex requirements fulfilled in larger and larger applications. Object-oriented programming provides one of the key methodologies in accomplishing this, to the point that it is difficult for object-oriented programmers to envision transitioning back to structured programming, except for the most trivial transitions.

The most fundamental construct to object-oriented programming is the class or object itself. These form a programming abstraction, model, or template of what is often a real-world concept. The class OpticalStorageMedia, for example, may have an Eject() method on it that causes a CD/DVD to eject from the player. The OpticalStorageMedia class is the programming abstraction of the real-world object of a CD.

Classes are the foundation for three principal characteristics of object-oriented programming: encapsulation, inheritance, and polymorphism.

## Encapsulation

Encapsulation allows you to hide detail. The detail can still be accessed when necessary, but by intelligently encapsulating the detail, large programs are easier to understand, data is protected from inadvertent modification, and code is easier to maintain because the effects of a code change are bound to the scope of the encapsulation. Methods are examples of encapsulation. Although it is possible to take the code from a method and embed it directly inline with the caller's code, refactoring of code into a method provides encapsulation benefits.

## Inheritance

Consider the following example: A DVD is a type of optical media. It has a specific storage capacity along with the ability to hold a digital movie. A CD is also a type of optical media, but it has different characteristics. The copyright implementation on CDs is different from DVD copyright protection, and the storage capacity is different as well. Both CDs and DVDs are different from hard drives, USB drives, and floppy drives (remember those?). All fit into the category of storage media, but each has special characteristics, even for fundamental functions such as the supported filesystems and whether instances of the media are read-only or read-write.

Inheritance in object-oriented programming allows you to write "is a" relationships between these similar but different items. It is a reasonable assumption that a DVD "is a" type of storage media and that a CD "is a" type of storage media, and as such, that each has storage capacity.

Similarly, CDs and DVDs have "is a" relationships to the optical media type, which in turn has an "is a" relationship with the storage media type. If you define classes corresponding to each type of storage media mentioned, you will have defined a class hierarchy, which is a series of "is a" relationships. The base type, from which all storage media derive, could be the class StorageMedia. As such, CDs, DVDs, hard drives, USB drives, and floppy drives are types of StorageMedia. However, CDs and DVDs don't need to derive from StorageMedia directly. Instead, they can derive from an intermediate type, OpticalStorageMedia. You can view the class hierarchy graphically using a Unified Modeling Language (UML)-like class diagram, as shown in Figure 5.1.

![](img/ef1bd88b5fdf5fb56f8510479607fe66_252_0.png)

Figure 5.1: Class Hierarchy

The inheritance relationship involves a minimum of two classes such that one class is a more general version of the other; in Figure 5.1, StorageMedia is a more general version of HardDrive. Although the more specialized type, HardDrive, is a type of StorageMedia, the reverse is not true; a StorageMedia type is not necessarily a HardDrive. As Figure 5.1 shows, inheritance can involve more than two classes.

The more specialized type is the derived type or the subtype. The more generalized type is the base class or sometimes the super type. Other common terms for the classes in an inheritance relationship are *parent* and *child*; the former is the more generalized class.

To **derive** or **inherit** from another type is to **specialize** that type, which means to customize the base type so that it is geared for a specific purpose. Similarly, the base type is the generalized implementation of the derived types.

The key feature of inheritance is that all derived types inherit the members of the base type. Often, the implementation of the base members can be modified, but regardless, the derived type contains the base type's members in addition to any other members that the derived type contains explicitly.

Derived types allow you to organize your classes into a coherent hierarchy where the "child" types have greater specificity than their "parent" types.

## Polymorphism

Polymorphism comprises a word meaning "many" and a word meaning "forms." In the context of objects, polymorphism means that a single method or type can have many forms of implementation. Suppose you have a media player. It follows that the media player could play both CD music discs and DVDs containing MP3s. However, the exact implementation of the Play() method will vary depending on the media type. Calling Play() on a music CD object or Play() on a music DVD will play music in both cases, because each type understands the intricacies of playing. All that the media player knows about is the common base type, opticalStorageMedia, and the fact that it defines the Play() method signature. Polymorphism is the principle that a type can take care of the exact details of a method's implementation because the method appears on multiple derived types that each share a common base type (or interface) that also contains the same method signature.

## Declaring and Instantiating a Class

Defining a class involves first specifying the keyword class, followed by an identifier, as shown in Listing 5.1.

## LISTING 5.1: Defining a Class

```
class Employee
{
}
```

All code that belongs to the class will appear between the curly braces following the class declaration. Although not a requirement, generally you place each class into its own file. This makes it easier to find the code that defines a particular class, because the convention is to name the file using the class name.

Once you have defined a new class, you can use that class as though it were built into the framework. In other words, you can declare a variable of that type or define a method that takes a parameter of the new class type. Listing 5.2 demonstrates.

## LISTING 5.2: Declaring Variables of the Class Type

```
class Program
{
    static void Main()
    {
        Employee employee1, employee2;
        // ...

    }

    static void IncreaseSalary (Employee employee)
    {
        // ...
    }
}
```

### BEGINNER TOPIC
### Objects and Classes Defined

In casual conversation, the terms class and object appear interchangeably. However, object and class have distinct meanings. A class is a template for what an object will look like at instantiation time. An object, therefore, is an instance of a class. Classes are like the mold for what a widget will look
