# Section 12.6.1 Pure Virtual Functions

+   - You create an abstract class by declaring one or more **pure virtual functions** (p. 548) with pure specifiers (`= 0`) in their declarations.
+   - If a class is derived from a class with a pure `virtual` function and that derived class does not supply a definition for that pure `virtual` function, then that `virtual` function remains pure in the derived class. Consequently, the derived class is also an abstract class.
+   - Although we cannot instantiate objects of abstract base classes, we can declare pointers and references to objects of abstract base classes. Such pointers and references can be used to enable polymorphic manipulations of derived-class objects instantiated from concrete derived classes.