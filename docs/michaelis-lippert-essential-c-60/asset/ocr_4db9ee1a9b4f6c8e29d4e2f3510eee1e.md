kind of” relationships. The base class, from which all storage devices derive, could be the class `StorageMedia`. As such, classes that represent CD drives, DVD drives, hard drives, USB drives, and floppy drives are derived from the class `StorageMedia`. However, the classes for CD and DVD drives don’t need to derive from `StorageMedia` directly. Instead, they can derive from an intermediate class, `OpticalStorageMedia`. You can view the class hierarchy graphically using a Unified Modeling Language (UML)–like class diagram, as shown in Figure 5.1.

![](bbox=[0.135, 0.321, 0.808, 0.595])

**FIGURE 5.1: Class Hierarchy**

The inheritance relationship involves a minimum of two classes, such that one class is a more specific kind of the other; in Figure 5.1, `HardDrive` is a more specific kind of `StorageMedia`. Although the more specialized type, `HardDrive`, is a kind of `StorageMedia`, the reverse is not true—that is, an instance of `StorageMedia` is not necessarily a `HardDrive`. As Figure 5.1 shows, inheritance can involve more than two classes.

The more specialized type is called **the derived type** or **the subtype**. The more general type is called **the base type** or **the super type**. The base type is also often called the “parent” type and its derived types are often called its “child” types. Though this usage is common, it can be confusing: After all, a child is not a kind of parent! In this book we will stick to “derived type” and “base type.”