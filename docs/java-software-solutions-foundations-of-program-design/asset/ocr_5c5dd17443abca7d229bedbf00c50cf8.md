characteristics: They are warmblooded, have hair, and produce milk to feed their young. Now consider a subset of mammals, such as horses. All horses are mammals and have all of the characteristics of mammals, but they also have unique features that make them different from other mammals such as dogs.

If we translate this idea into software terms, an existing class called Mammal would have certain variables and methods that describe the state and behavior of mammals. A Horse class could be derived from the existing Mammal class, automatically inheriting the variables and methods contained in Mammal. The Horse class can refer to the inherited variables and methods as if they had been declared locally in that class. New variables and methods can then be added to the derived class to distinguish a horse from other mammals.

The original class that is used to derive a new one is called the parent class, superclass, or base class. The derived class is called a child class, or subclass. Java uses the reserved word extends to indicate that a new class is being derived from an existing class.

The process of inheritance should establish an is-a relationship between two classes. That is, the child class should be a more specific version of the parent. For example, a horse is a mammal. Not all mammals are horses, but all horses are mammals. For any class X that is derived from class Y, you should be able to say that “X is a Y.” If such a statement doesn’t make sense, then that relationship is probably not an appropriate use of inheritance.

Let’s look at an example. The program shown in Listing 9.1 instantiates an object of class Dictionary, which is derived from a class called Book. In the main method, three methods are invoked through the Dictionary object: two that were declared locally in the Dictionary class and one that was inherited from the Book class.

The Book class (see Listing 9.2) is used to derive the Dictionary class (see Listing 9.3) using the reserved word extends in the header of Dictionary. The Dictionary class automatically inherits the definition of the setPages and getPages methods, as well as the pages variable. It is as if those methods and the pages variable were declared inside the Dictionary class. Note that, in the Dictionary class, the computeRatio method explicitly references the pages variable, even though the variable is declared in the Book class.

Also note that although the Book class is needed to create the definition of Dictionary, no Book object is ever instantiated in the program. An instance of a child class does not rely on an instance of the parent class.

Inheritance is a one-way street. The Book class cannot use variables or methods that are declared explicitly in the Dictionary class. For instance, if we created an object from the Book class, it could not be used to invoke the setDefinitions method. This restriction makes sense, because a child class is a more specific

KEY CONCEPT
Inheritance creates an is-a relationship between the parent and child classes.