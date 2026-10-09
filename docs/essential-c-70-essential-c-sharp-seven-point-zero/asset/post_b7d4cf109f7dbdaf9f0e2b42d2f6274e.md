
The most fundamental construct in object-oriented programming is the class. A group of classes forms a programming abstraction, model, or template of what is often a real-world concept. The class `OpticalStorageMedia`, for example, may have an `Eject()` method on it that causes a disk to eject from the player. The `OpticalStorageMedia` class is the programming abstraction of the real-world object of a CD or DVD player.

Classes exhibit the three principal characteristics of object-oriented programming: encapsulation, inheritance, and polymorphism.

## Encapsulation

Encapsulation allows you to hide details. The details can still be accessed when necessary, but by intelligently encapsulating the details, large programs are made easier to understand, data is protected from inadvertent modification, and code becomes easier to maintain because the effects of a code change are limited to the scope of the encapsulation. Methods are examples of encapsulation. Although it is possible to take the code from a method and embed it directly inline with the caller’s code, refactoring of code into a method provides encapsulation benefits.

## Inheritance

Consider the following example: A DVD drive is a type of optical media device. It has a specific storage capacity along with the ability to hold a digital movie. A CD drive is also a type of optical media device, but it has different characteristics. The copy protection on CDs is different from DVD copy protection, and the storage capacity is different as well. Both CD drives and DVD drives are different from hard drives, USB drives, and floppy drives (remember those?). All fit into the category of storage devices, but each has special characteristics, even for fundamental functions such as the supported filesystems and whether instances of the media are read-only or read/write.

Inheritance in object-oriented programming allows you to form “is a kind of” relationships between these similar but different items. It is reasonable to say that a DVD drive “is a kind of” storage media and that a CD drive “is a kind of” storage media, and as such, each has storage capacity. We could also reasonably say that both have an “is a kind of” relationship with “optical storage media,” which in turn “is a kind of” storage media.

If you define classes corresponding to each type of storage device mentioned, you will have defined a **class hierarchy**, which is a series of “is a kind of” relationships. The base class, from which all storage devices derive, could be the class *StorageMedia*. As such, classes that represent CD drives, DVD drives, hard drives, USB drives, and floppy drives are derived from the class *StorageMedia*. However, the classes for CD and DVD drives don’t need to derive from *StorageMedia* directly. Instead, they can derive from an intermediate class, *OpticalStorageMedia*. You can view the class hierarchy graphically using a Unified Modeling Language (UML)–like class diagram, as shown in Figure 6.1.

![](img/ef6a8a417630b222bfb3f3b949facff0_280_0.png)

**FIGURE 6.1: Class Hierarchy**

The inheritance relationship involves a minimum of two classes, such that one class is a more specific kind of the other; in Figure 6.1, *HardDrive* is a more specific kind of *StorageMedia*. Although the more specialized type, *HardDrive*, is a kind of *StorageMedia*, the reverse is not true—that is, an instance of *StorageMedia* is not necessarily a *HardDrive*. As Figure 6.1 shows, inheritance can involve more than two classes.

The more specialized type is called the **derived type** or the **subtype**. The more general type is called the **base type** or the **supertype**. The base type is also often called the *parent* type, and its derived types are often called its *child* types. Though this usage is common, it can be confusing: After all, a child is not a kind of parent! In this book, we stick to *derived type* and *base type*.

To derive or inherit from another type is to specialize that type, which means to customize the base type so that it is more suitable for a specific purpose. The base type may contain those implementation details that are common to all of the derived types.

The key feature of inheritance is that all derived types inherit the members of the base type. Often, the implementation of the base members can be modified, but regardless, the derived type contains the base type's members in addition to any other members that the derived type contains explicitly.

Derived types allow you to organize your classes into a coherent hierarchy where the derived types have greater specificity than their base types.

## Polymorphism

Polymorphism is formed from poly, meaning “many,” and morph, meaning “form.” In the context of objects, polymorphism means that a single method or type can have many forms of implementation.

Suppose you have a media player that can play both music CDs and DVDs containing MP3s. However, the exact implementation of the `Play()` method will vary depending on the media type. Calling `Play()` on an object representing a music CD or on an object representing a music DVD will play music in both cases, because each object’s type understands the intricacies of playing. All that the media player knows about is the common base type, `OpticalStorageMedia`, and the fact that it defines the `Play()` method. Polymorphism is the principle that a type can take care of the exact details of a method’s implementation because the method appears on multiple derived types, each of which shares a common base type (or interface) that also contains the same method signature.

## Declaring and Instantiating a Class

Defining a class involves first specifying the keyword `class`, followed by an identifier, as shown in Listing 6.1.

### LISTING 6.1: Defining a Class

```text
class Employee
{
}
```

All code that belongs to the class will appear between the curly braces following the class declaration. Although not a requirement, generally you place each class into its own file. This makes it easier to find the code that defines a particular class, because the convention is to name the file using the class name.

### Guidelines

- **DO NOT** place more than one class in a single source file.
- **DO** name the source file with the name of the public type it contains.

Once you have defined a new class, you can use that class as though it were built into the framework. In other words, you can declare a variable of that type or define a method that takes a parameter of the new class type. Listing 6.2 demonstrates such declarations.

### LISTING 6.2: Declaring Variables of the Class Type

```csharp
class Program
{
    static void Main()
    {
        Employee employee1, employee2;
        // ...
    }

    static void IncreaseSalary(Employee employee)
    {
        // ...
    }
}
```

## BEGINNER TOPIC

### Objects and Classes Defined

In casual conversation, the terms *class* and *object* appear interchangeably. However, object and class have distinct meanings. A **class** is a template for what an object will look like at instantiation time. An **object**, therefore, is an instance of a class. Classes are like the mold for what a widget will look like. Objects correspond to widgets created by the mold. The process of creating an object from a class is called **instantiation** because an object is an instance of a class.

Now that you have defined a new class type, it is time to instantiate an object of that type. Mimicking its predecessors, C# uses the `new` keyword to instantiate an object (see Listing 6.3).

### LISTING 6.3: Instantiating a Class

```csharp
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        Employee employee2;
        employee2 = new Employee();
        
        IncreaseSalary(employee1);
    }
}
```

Not surprisingly, the assignment can occur in the same statement as the declaration or in a separate statement.

Unlike the primitive types you have worked with so far, there is no literal way to specify an `Employee`. Instead, the **new** operator provides an instruction to the runtime to allocate memory for an `Employee` object, instantiate the object, and return a reference to the instance.

Although an explicit operator for allocating memory exists, there is no such operator for de-allocating the memory. Instead, the runtime automatically reclaims the memory sometime after the object becomes inaccessible. The **garbage collector** is responsible for the automatic de-allocation. It determines which objects are no longer referenced by other active objects and then de-allocates the memory for those objects. The result is that there is no compile-time–determined program location where the memory will be collected and restored to the system.

In this trivial example, no explicit data or methods are associated with an `Employee`, which renders the object essentially useless. The next section focuses on adding data to an object.
