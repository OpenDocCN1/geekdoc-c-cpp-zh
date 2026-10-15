# Summary of Key Concepts

+   - Inheritance is the process of deriving a new class from an existing one.
+   - One purpose of inheritance is to reuse existing software.
+   - Inheritance creates an is-a relationship between the parent and child classes.
+   - Protected visibility provides the best possible encapsulation that permits inheritance.
+   - A parent’s constructor can be invoked using the `super` reference.
+   - A child class can override (redefine) the parent’s definition of an inherited method.
+   - The child of one class can be the parent of one or more other classes, creating a class hierarchy.
+   - Common features should be located as high in a class hierarchy as is reasonably possible.
+   - All Java classes are derived, directly or indirectly, from the `Object` class.
+   - The `toString` and `equals` methods are inherited by every class in every Java program.
+   - An abstract class cannot be instantiated. It represents a concept on which other classes can build their definitions.
+   - A class derived from an abstract parent must override all of its parent’s abstract methods, or the derived class will also be considered abstract.
+   - Inheritance can be applied to interfaces so that one interface can be derived from another.
+   - Private members are inherited by the child class, but cannot be referenced directly by name. They may be used indirectly, however.
+   - Software design must carefully and specifically address inheritance.
+   - The `final` modifier can be used to restrict inheritance.
+   - The classes that represent Java GUI components are organized into a class hierarchy.
+   - A listener class can be created by deriving it from an event adapter class.
+   - A `Timer` object generates action events at regular intervals and can be used to control an animation.