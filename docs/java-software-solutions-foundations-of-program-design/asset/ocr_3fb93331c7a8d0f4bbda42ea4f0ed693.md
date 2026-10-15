object’s class name followed by a numeric value that is unique for that object. Usually, we override the Object version of toString to fit our own needs. The String class has overridden the toString method so that it returns its stored string value.

We are also overriding an inherited method when we define an equals method for a class. As we’ve discussed previously, the purpose of the equals method is to determine whether two objects are equal. The definition of the equals method provided by the Object class returns true if the two object references actually refer to the same object (that is, if they are aliases). Classes often override the inherited definition of the equals method in favor of a more appropriate definition. For instance, the String class overrides equals so that it returns true only if both strings contain the same characters in the same order.

# Abstract Classes

An abstract class represents a generic concept in a class hierarchy. An abstract class cannot be instantiated and usually contains one or more abstract methods, which have no definition. We’ve discussed abstract methods in Chapter 7 when they are used to define a Java interface. An abstract class is similar to an interface in some ways. However, unlike interfaces, an abstract class can contain methods that are not abstract. It can also contain data declarations other than constants.

A class is declared as abstract by including the abstract modifier in the class header. Any class that contains one or more abstract methods must be declared as abstract. In abstract classes (unlike interfaces), the abstract modifier must be applied to each abstract method. A class declared as abstract does not have to contain abstract methods.

> KEY CONCEPT
> An abstract class cannot be instantiated. It represents a concept on which other classes can build their definitions.

Abstract classes serve as placeholders in a class hierarchy. As the name implies, an abstract class represents an abstract entity that is usually insufficiently defined to be useful by itself. Instead, an abstract class may contain a partial description that is inherited by all of its descendants in the class hierarchy. Its children, which are more specific, fill in the gaps.

Consider the class hierarchy shown in Figure 9.6. The Vehicle class at the top of the hierarchy may be too generic for a particular application. Therefore we may choose to implement it as an abstract class. In UML diagrams, abstract class names are shown in italic.

Concepts that apply to all vehicles can be represented in the Vehicle class and are inherited by its descendants. That way, each of its descendants doesn’t have to define the same concept redundantly (and perhaps inconsistently). For example, we may say that all vehicles have a particular speed. Therefore we declare a speed variable in the Vehicle class, and all specific vehicles below it in the hierarchy

VideoNote
Example using a class hierarchy.