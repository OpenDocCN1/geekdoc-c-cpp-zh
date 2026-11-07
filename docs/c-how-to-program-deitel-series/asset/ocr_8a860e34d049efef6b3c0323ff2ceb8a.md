+   - With polymorphism, we can design and implement systems that are easily extensible—new classes can be added with little or no modification to the general portions of the program. The only parts of a program that must be altered to accommodate new classes are those that require direct knowledge of the new classes that you add to the hierarchy.

# Section 12.2 Introduction to Polymorphism: Polymorphic Video Game

+   - With polymorphism, one function call can cause different actions to occur, depending on the type of the object on which the function is invoked.
+   - This makes it possible to design and implement more extensible systems. Programs can be written to process objects of types that may not exist when the program is under development.

# Section 12.3 Relationships Among Objects in an Inheritance Hierarchy

+   - C++ enables polymorphism—the ability for objects of different classes related by inheritance to respond differently to the same member-function call.
+   - Polymorphism is implemented via virtual functions (p. 526) and dynamic binding (p. 527).
+   - When a base-class pointer or reference is used to call a virtual function, C++ chooses the correct overridden function in the appropriate derived class associated with the object.
+   - If a virtual function is called by referencing a specific object by name and using the dot member-selection operator, the reference is resolved at compile time (this is called static binding; p. 527); the virtual function that is called is the one defined for the class of that particular object.
+   - Derived classes can override a base-class virtual function if necessary, but if they do not, the base class’s implementation is used.
+   - Declare the base-class destructor virtual (p. 532) if the class contains virtual functions. This makes all derived-class destructors virtual, even though they do not have the same name as the base-class destructor. If an object in the hierarchy is destroyed explicitly by applying the delete operator to a base-class pointer to a derived-class object, the destructor for the appropriate class is called. After a derived-class destructor runs, the destructors for all of that class’s base classes run all the way up the hierarchy.

# Section 12.4 Type Fields and switch Statements

+   - Polymorphic programming with virtual functions can eliminate the need for switch logic. You can use the virtual function mechanism to perform the equivalent logic automatically, thus avoiding the kinds of errors typically associated with switch logic.

# Section 12.5 Abstract Classes and Pure Virtual Functions

+   - Abstract classes (p. 533) are typically used as base classes, so we refer to them as abstract base classes (p. 533). No objects of an abstract class may be instantiated.
+   - Classes from which objects can be instantiated are concrete classes (p. 533).
+   - You create an abstract class by declaring one or more pure virtual functions (p. 534) with pure specifiers (= 0) in their declarations.
+   - If a class is derived from a class with a pure virtual function and that derived class does not supply a definition for that pure virtual function, then that virtual function remains pure in the derived class. Consequently, the derived class is also an abstract class.
+   - Although we cannot instantiate objects of abstract base classes, we can declare pointers and references to objects of abstract base classes. Such pointers and references can be used to enable polymorphic manipulations of derived-class objects instantiated from concrete derived classes.