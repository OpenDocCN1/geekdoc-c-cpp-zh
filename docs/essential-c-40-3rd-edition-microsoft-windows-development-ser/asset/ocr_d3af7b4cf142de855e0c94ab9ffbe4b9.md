fulfilled in larger and larger applications. Object-oriented programming provides one of the key methodologies in accomplishing this, to the point that it is difficult for object-oriented programmers to envision transitioning back to structured programming, except for the most trivial transitions.

The most fundamental construct to object-oriented programming is the class or object itself. These form a programming abstraction, model, or template of what is often a real-world concept. The class OpticalStorageMedia, for example, may have an Eject() method on it that causes a CD/DVD to eject from the player. The OpticalStorageMedia class is the programming abstraction of the real-world object of a CD.

Classes are the foundation for three principal characteristics of object-oriented programming: encapsulation, inheritance, and polymorphism.

# Encapsulation

Encapsulation allows you to hide detail. The detail can still be accessed when necessary, but by intelligently encapsulating the detail, large programs are easier to understand, data is protected from inadvertent modification, and code is easier to maintain because the effects of a code change are bound to the scope of the encapsulation. Methods are examples of encapsulation. Although it is possible to take the code from a method and embed it directly inline with the caller’s code, refactoring of code into a method provides encapsulation benefits.

# Inheritance

Consider the following example: A DVD is a type of optical media. It has a specific storage capacity along with the ability to hold a digital movie. A CD is also a type of optical media, but it has different characteristics. The copyright implementation on CDs is different from DVD copyright protection, and the storage capacity is different as well. Both CDs and DVDs are different from hard drives, USB drives, and floppy drives (remember those?). All fit into the category of storage media, but each has special characteristics, even for fundamental functions such as the supported filesystems and whether instances of the media are read-only or read-write.

Inheritance in object-oriented programming allows you to write “is a” relationships between these similar but different items. It is a reasonable assumption that a DVD “is a” type of storage media and that a CD “is a” type of storage media, and as such, that each has storage capacity.