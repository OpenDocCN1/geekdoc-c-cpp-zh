
method that returns a string as follows: “Pre-school” if the target age is 4 through 6, “Early” if the target age is 7 through 9, “Middle” if the target age is 10 through 12, and “Upper” if the target age is 13 through 16.

SR 9.7  What is the difference between single inheritance and multiple inheritance?

## 9.2 Overriding Methods

When a child class defines a method with the same name and signature as a method in the parent class, we say that the child’s version *overrides* the parent’s version in favor of its own. The need for overriding occurs often in inheritance situations.

The program in Listing 9.7 provides a simple demonstration of method overriding in Java. The Messages class contains a main method that instantiates two objects: one from class Thought and one from class Advice. The Thought class is the parent of the Advice class.

> **KEY CONCEPT**
> 
> A child class can override (redefine) the parent’s definition of an inherited method.

```java
//********************************************************************
//  Messages.java              Author: Lewis/Loftus
//
//  Demonstrates the use of an overridden method.
//********************************************************************
public class Messages
{
   //-----------------------------------------------------------------
   //  Creates two objects and invokes the message method in each.
   //-----------------------------------------------------------------
   public static void main (String[] args)
   {
      Thought parked = new Thought();
      Advice dates = new Advice();

      parked.message();

      dates.message();  // overridden
   }
}
```

### LISTING 9.7 continued
OUTPUT

```
I feel like I'm diagonally parked in a parallel universe.

Warning: Dates in calendar are closer than they appear.

I feel like I'm diagonally parked in a parallel universe.
```

Both the Thought class (see Listing 9.8) and the Advice class (see Listing 9.9) contain a definition for a method called message. The version of message defined in the Thought class is inherited by Advice, but Advice overrides it with an alternative version. The new version of the method prints out an entirely different message and then invokes the parent’s version of the message method using the super reference.

The object that is used to invoke a method determines which version of the method is actually executed. When message is invoked using the parked object in

### LISTING 9.8

```
//****************************************************************
// Thought.java      Author: Lewis/Loftus
//
// Represents a stray thought. Used as the parent of a derived
// class to demonstrate the use of an overridden method.
//****************************************************************

public class Thought
{
    //-------------------------------------------------------------
    // Prints a message.
    //-------------------------------------------------------------
    public void message()
    {
        System.out.println ("I feel like I'm diagonally parked in a " +
                            "parallel universe.");

        System.out.println();
    }
}
```

```java
// Advice.java Author: Lewis/Loftus
// Represents some thoughtful advice. Used to demonstrate the use
// of an overridden method.
public class Advice extends Thought
{
// Prints a message. This method overrides the parent's version.
// public void message()
{
System.out.println("Warning: Dates in calendar are closer " +
"than they appear.");
System.out.println();
super.message(); // explicitly invokes the parent's version
}
}
```

the main method, the Thought version of message is executed. When message is invoked using the dates object, the Advice version of message is executed.

A method can be defined with the final modifier. A child class cannot over-ride a final method. This technique is used to ensure that a derived class uses a particular definition of a particular method.

Method overriding is a key element in object-oriented design. It allows two objects that are related by inheritance to use the same naming conventions for methods that accomplish the same general task in different ways. Overriding becomes even more important when it comes to polymorphism, which is discussed in Chapter 10.

## Shadowing Variables

It is possible, although not recommended, for a child class to declare a variable with the same name as one that is inherited from the parent. Note the distinction between redeclaring a variable and simply giving an inherited variable a particular value. If a variable of the same name is declared in a child class, it is called a shadow variable. It is similar in concept to the process of overriding methods but creates confusing subtleties.

Because an inherited variable is already available to the child class, there is usually no good reason to redeclare it. Someone reading code with a shadowed variable will find two different declarations that seem to apply to a variable used in the child class. This confusion causes problems and serves no useful purpose. A redeclaration of a particular variable name could change its type, but that is usually unnecessary. In general, shadowing variables should be avoided.

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

SR 9.8 Why would a child class override one or more of the methods of its parent class?

SR 9.9 True or False? Explain.

- a. A child class may define a method with the same name as a method in the parent class.
- b. A child class can override the constructor of the parent class.
- c. A child class can override a final method of the parent class.
- d. It is considered poor design when a child class overrides a method from the parent class.
- e. A child class may define a variable with the same name as a variable in the parent class.

## 9.3 Class Hierarchies

A child class derived from one parent can be the parent of its own child class. Furthermore, multiple classes can be derived from a single parent. Therefore, inheritance relationships often develop into class hierarchies. The diagram in Figure 9.3 shows a class

> KEY CONCEPT
> The child of one class can be the parent of one or more other classes, creating a class hierarchy.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_485_0.png)

FIGURE 9.3 A UML class diagram showing a class hierarchy

hierarchy that includes the inheritance relationship between the Mammal and Horse classes.

There is no limit to the number of children a class can have or to the number of levels to which a class hierarchy can extend. Two children of the same parent are called siblings. Although siblings share the characteristics passed on by their common parent, they are not related by inheritance, because one is not used to derive the other.

In class hierarchies, common features should be kept as high in the hierarchy as reasonably possible. That way, the only characteristics explicitly established in a child class are those that make the class distinct from its parent and from its siblings. This approach maximizes the potential to reuse classes. It also facilitates maintenance activities, because when changes are made to the parent, they are automatically reflected in the descendents. Always remember to maintain the is-a relationship when building class hierarchies.

The inheritance mechanism is transitive. That is, a parent passes along a trait to a child class, and that child class passes it along to its children, and so on. An inherited feature might have originated in the immediate parent or possibly several levels higher in a more distant ancestor class.

> KEY CONCEPT
> Common features should be located as high in a class hierarchy as is reasonably possible.

There is no single best hierarchy organization for all situations. The decisions you make when you are designing a class hierarchy restrict and guide more detailed design decisions and implementation options, so you must make them carefully.

Earlier in this chapter we discussed a class hierarchy that organized animals by their major biological classifications, such as Mammal, Bird, and Reptile. However, in a different situation, the same animals might logically be organized in a different way. For example, as shown in Figure 9.4, the class hierarchy might be organized around a function of the animals, such as their ability to fly. In this case, a Parrot class and a Bat class would be siblings derived from a general FlyingAnimal class. This class hierarchy is as valid and reasonable as the original one. The needs of the programs that use the classes will determine which is best for the particular situation.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_486_0.png)

FIGURE 9.4 An alternative hierarchy for organizing animals
