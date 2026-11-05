Now any and every class that derives from the Person class must provide the implementation details for the GetExerciseHabits() method. That is what adding the abstract keyword does. It is like signing a contract. If you derive from an abstract base class, you sign a contract that details how to implement its abstract methods.

> NOTE
> You will receive a syntax error if you use the keyword static or virtual when defining an abstract method. There is an implicit assumption that the method will be overridden; thus, the keyword virtual is unnecessary in the base class.

If the abstract class includes more than one abstract method, derived classes must provide implementation details for every abstract method included in the base class. Abstract classes can include regular data field members, regular methods, and virtual methods in addition to abstract methods. Remember that a virtual method tags the method as being capable of being overridden in a derived class. This does not mean that all derived classes have to provide new implementation details for those tagged as virtual, just that they can.

In the derived class, all abstract methods' headings include the special keyword override. Thus, the only change needed for the Student class is a new method, GetExerciseHabits(), which has an override keyword added to the method heading. The method body must return a string argument. You can see that new method if you look ahead to Example 11-21, which illustrates the completed Student class.

All .NET languages only support single inheritance, which means that a class can extend or derive from at most one class. One-way languages such as C# and Java work around this is by implementing multiple interfaces, which are the topic for the next section.

> NOTE
> C++ permits multiple inheritances. A class can extend from more than one base class in C++. This is not possible in C#, Java, or any of the managed .NET languages.

# Sealed Classes

You learned that the abstract keyword enables you to create a class solely for the purpose of inheritance. Abstract classes cannot be instantiated. Objects can only be created using classes derived from the abstract class. The purpose of an abstract class is to provide a common definition of a base class so that multiple derived classes can share that definition. Sealed classes provide a completely opposite type of restriction. They restrict the inheritance feature of object-oriented programming. When you add the modifier sealed to a class, the class cannot be a base class. In order to define a sealed class, add the keyword sealed following the access modifier as shown in Example 11-18.