
# 5
Classes

YOU BRIEFLY SAW IN CHAPTER 1 how to declare a new class called HelloWorld. In Chapter 2, you learned about the built-in primitive types included with C#. Since you have now also learned about control flow and how to declare methods, it is time to discuss defining your own types. This is the core construct of any C# program; this support for classes and the objects created from them is what makes C# an object-oriented language.

![](img/25683ccec0773ba5b8794b11f2b12877_255_0.png)

## Chapter 5: Classes

This chapter introduces the basics of object-oriented programming using C#. A key focus is on how to define **classes**, which are the templates for objects themselves.

All of the constructs of structured programming from the previous chapters still apply within object-oriented programming. However, by wrapping those constructs within classes, you can create larger, more organized programs that are more maintainable. The transition from structured, control-flow-based programs to object-oriented programs revolutionized programming because it provided an extra level of organization. The result was that smaller programs were simplified somewhat. Even more importantly, it was easier to create much larger programs because the code within those programs was better organized.

One of the key advantages of object-oriented programming is that instead of creating new programs entirely from scratch, you can assemble a collection of existing objects from prior work, extending the classes with new features, adding more classes, and thereby providing new functionality.

Readers unfamiliar with object-oriented programming should read the Beginner Topic blocks for an introduction. The general text outside the Beginner Topics focuses on using C# for object-oriented programming with the assumption that readers are already familiar with object-oriented concepts.

This chapter delves into how C# supports encapsulation through its support of constructs such as classes, properties, and access modifiers; we covered methods in the preceding chapter. The next chapter builds on this foundation with the introduction of inheritance and the polymorphism that object-oriented programming enables.

### BEGINNER TOPIC

### Object-Oriented Programming

The key to programming successfully today lies in the ability to provide organization and structure to the implementation of the complex requirements of large applications. Object-oriented programming provides one of the key methodologies in accomplishing this goal, to the point that it is difficult for object-oriented programmers to envision transitioning back to structured programming, except for the most trivial programs.

The most fundamental construct in object-oriented programming is the class. A group of classes form a programming abstraction, model, or template of what is often a real-world concept. The class OpticalStorageMedia, for example, may have an Eject() method on it that causes a disk to eject from the player. The OpticalStorageMedia class is the programming abstraction of the real-world object of a CD or DVD player.

Classes exhibit the three principal characteristics of object-oriented programming: encapsulation, inheritance, and polymorphism.

### Encapsulation

Encapsulation allows you to hide details. The details can still be accessed when necessary, but by intelligently encapsulating the details, large programs are made easier to understand, data is protected from inadvertent modification, and code becomes easier to maintain because the effects of a code change are limited to the scope of the encapsulation. Methods are examples of encapsulation. Although it is possible to take the code from a method and embed it directly inline with the caller’s code, refactoring of code into a method provides encapsulation benefits.

### Inheritance

Consider the following example: A DVD drive is a type of optical media device. It has a specific storage capacity along with the ability to hold a digital movie. A CD drive is also a type of optical media device, but it has different characteristics. The copy protection on CDs is different from DVD copy protection, and the storage capacity is different as well. Both CD drives and DVD drives are different from hard drives, USB drives, and floppy drives (remember those?). All fit into the category of storage devices, but each has special characteristics, even for fundamental functions such as the supported filesystems and whether instances of the media are read-only or read/write.

Inheritance in object-oriented programming allows you to form “is a kind of” relationships between these similar but different items. It is reasonable to say that a DVD drive “is a kind of” storage media and that a CD drive “is a kind of” storage media, and as such, that each has storage capacity. We could also reasonably say that both have an “is a kind of” relationship with “optical storage media,” which in turn “is a kind of” storage media.

If you define classes corresponding to each type of storage device mentioned, you will have defined a class hierarchy, which is a series of “is a kind of” relationships. The base class, from which all storage devices derive, could be the class `StorageMedia`. As such, classes that represent CD drives, DVD drives, hard drives, USB drives, and floppy drives are derived from the class `StorageMedia`. However, the classes for CD and DVD drives don’t need to derive from `StorageMedia` directly. Instead, they can derive from an intermediate class, `OpticalStorageMedia`. You can view the class hierarchy graphically using a Unified Modeling Language (UML)–like class diagram, as shown in Figure 5.1.

![](img/25683ccec0773ba5b8794b11f2b12877_258_0.png)

**FIGURE 5.1: Class Hierarchy**

The inheritance relationship involves a minimum of two classes, such that one class is a more specific kind of the other; in Figure 5.1, `HardDrive` is a more specific kind of `StorageMedia`. Although the more specialized type, `HardDrive`, is a kind of `StorageMedia`, the reverse is not true—that is, an instance of `StorageMedia` is not necessarily a `HardDrive`. As Figure 5.1 shows, inheritance can involve more than two classes.

The more specialized type is called **the derived type** or **the subtype**. The more general type is called **the base type** or **the super type**. The base type is also often called the “parent” type and its derived types are often called its “child” types. Though this usage is common, it can be confusing: After all, a child is not a kind of parent! In this book we will stick to “derived type” and “base type.”

To **derive** or **inherit** from another type is to **specialize** that type, which means to customize the base type so that it is more suitable for a specific purpose. The base type may contain those implementation details that are common to all of the derived types.

The key feature of inheritance is that all derived types inherit the members of the base type. Often, the implementation of the base members can be modified, but regardless, the derived type contains the base type’s members in addition to any other members that the derived type contains explicitly.

Derived types allow you to organize your classes into a coherent hierarchy where the derived types have greater specificity than their base types.

### Polymorphism

**Polymorphism** is formed from *poly*, meaning “many,” and *morph*, meaning “form.” In the context of objects, polymorphism means that a single method or type can have many forms of implementation.

Suppose you have a media player that can play both CD music discs and DVDs containing MP3s. However, the exact implementation of the Play() method will vary depending on the media type. Calling Play() on an object representing a music CD or on an object representing a music DVD will play music in both cases, because each object’s type understands the intricacies of playing. All that the media player knows about is the common base type, OpticalStorageMedia, and the fact that it defines the Play() method. Polymorphism is the principle that a type can take care of the exact details of a method’s implementation because the method appears on multiple derived types, each of which shares a common base type (or interface) that also contains the same method signature.

### Declaring and Instantiating a Class

Defining a class involves first specifying the keyword class, followed by an identifier, as shown in Listing 5.1.

### LISTING 5.1: Defining a Class

```
class Employee
{
}
```

All code that belongs to the class will appear between the curly braces following the class declaration. Although not a requirement, generally you
