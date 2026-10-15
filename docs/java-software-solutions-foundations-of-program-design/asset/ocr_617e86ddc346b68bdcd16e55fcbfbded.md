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
```

the main method, the Thought version of message is executed. When message is invoked using the dates object, the Advice version of message is executed.

A method can be defined with the final modifier. A child class cannot over-ride a final method. This technique is used to ensure that a derived class uses a particular definition of a particular method.

Method overriding is a key element in object-oriented design. It allows two objects that are related by inheritance to use the same naming conventions for methods that accomplish the same general task in different ways. Overriding becomes even more important when it comes to polymorphism, which is discussed in Chapter 10.

# Shadowing Variables

It is possible, although not recommended, for a child class to declare a variable with the same name as one that is inherited from the parent. Note the distinction between redeclaring a variable and simply giving an inherited variable a particular value. If a variable of the same name is declared in a child class, it is called a shadow variable. It is similar in concept to the process of overriding methods but creates confusing subtleties.