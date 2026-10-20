
for ImageIcon receives a String that specifies the path to the image. Since we specify only a file name, Java assumes that it’s in the same directory as class LabelDemo. ImageIcon can load images in GIF, JPEG and PNG image formats. Line 19 declares and initializes local variable centerLabel with a JLabel that displays the labelIcon. Line 22 declares and initializes local variable southLabel with a JLabel similar to the one in line 19. However, line 25 calls method setText to change the text the label displays. Method setText can be called on any JLabel to change its text. This JLabel displays both the icon and the text.

Line 28 creates the JFrame that displays the JLabels, and line 30 indicates that the program should terminate when the JFrame is closed. We attach the labels to the JFrame in lines 34–36 by calling an overloaded version of method add that takes two parameters. The first parameter is the component we want to attach, and the second is the region in which it should be placed. Each JFrame has an associated layout that helps the JFrame position the GUI components that are attached to it. The default layout for a JFrame is known as a BorderLayout and has five regions—NORTH (top), SOUTH (bottom), EAST (right side), WEST (left side) and CENTER. Each of these is declared as a constant in class BorderLayout. When calling method add with one argument, the JFrame places the component in the CENTER automatically. If a position already contains a component, then the new component takes its place. Lines 38 and 39 set the size of the JFrame and make it visible on screen.

## GUI and Graphics Case Study Exercise

9.1 Modify GUI and Graphics Case Study Exercise 8.1 to include a JLabel as a status bar that displays counts representing the number of each shape displayed. Class DrawPanel should declare a method that returns a String containing the status text. In main, first create the DrawPanel, then create the JLabel with the status text as an argument to the JLabel’s constructor. Attach the JLabel to the SOUTH region of the JFrame, as shown in Fig. 9.14.

![](img/009e962758dcc71dbc43a493362e6dc0_427_0.png)

Fig. 9.14 | JLabel displaying shape statistics.

## 9.9 Wrap-Up

This chapter introduced inheritance—the ability to create classes by absorbing an existing class’s members and embellishing them with new capabilities. You learned the notions of superclasses and subclasses and used keyword extends to create a subclass that inherits members from a superclass. We showed how to use the @Override annotation to prevent unintended overloading by indicating that a method overrides a superclass method. We introduced the access modifier protected; subclass methods can directly access protected superclass members. You learned how to use super to access overridden superclass members. You also saw how constructors are used in inheritance hierarchies. Finally, you learned about the methods of class Object, the direct or indirect superclass of all Java classes.

In Chapter 10, Object-Oriented Programming: Polymorphism, we build on our discussion of inheritance by introducing polymorphism—an object-oriented concept that enables us to write programs that conveniently handle, in a more general manner, objects of a wide variety of classes related by inheritance. After studying Chapter 10, you’ll be familiar with classes, objects, encapsulation, inheritance and polymorphism—the key technologies of object-oriented programming.

## Summary

### Section 9.1 Introduction

- Inheritance (p. 360) reduces program-development time.
- The direct superclass (p. 360) of a subclass (specified by the keyword extends in the first line of a class declaration) is the superclass from which the subclass inherits. An indirect superclass (p. 360) of a subclass is two or more levels up the class hierarchy from that subclass.
- In single inheritance (p. 360), a class is derived from one direct superclass. In multiple inheritance, a class is derived from more than one direct superclass. Java does not support multiple inheritance.
- A subclass is more specific than its superclass and represents a smaller group of objects (p. 360).
- Every object of a subclass is also an object of that class’s superclass. However, a superclass object is not an object of its class’s subclasses.
- An is-a relationship (p. 361) represents inheritance. In an is-a relationship, an object of a subclass also can be treated as an object of its superclass.
- A has-a relationship (p. 361) represents composition. In a has-a relationship, a class object contains references to objects of other classes.

### Section 9.2 Superclasses and Subclasses

- Single-inheritance relationships form treelike hierarchical structures—a superclass exists in a hierarchical relationship with its subclasses.

### Section 9.3 protected Members

- A superclass’s public members are accessible wherever the program has a reference to an object of that superclass or one of its subclasses.
- A superclass’s private members can be accessed directly only within the superclass’s declaration.
- A superclass’s protected members (p. 363) have an intermediate level of protection between public and private access. They can be accessed by members of the superclass, by members of its subclasses and by members of other classes in the same package.
- A superclass’s private members are hidden in its subclasses and can be accessed only through the public or protected methods inherited from the superclass.
- An overridden superclass method can be accessed from a subclass if the superclass method name is preceded by super (p. 363) and a dot (.) separator.

### Section 9.4 Relationship between Superclasses and Subclasses

- A subclass cannot access the private members of its superclass, but it can access the non-private members.
- A subclass can invoke a constructor of its superclass by using the keyword super, followed by a set of parentheses containing the superclass constructor arguments. This must appear as the first statement in the subclass constructor’s body.
- A superclass method can be overridden in a subclass to declare an appropriate implementation for the subclass.
- The annotation @override (p. 368) indicates that a method should override a superclass method. When the compiler encounters a method declared with @override, it compares the method’s signature with the superclass’s method signatures. If there isn’t an exact match, the compiler issues an error message, such as “method does not override or implement a method from a supertype.”
- Method toString takes no arguments and returns a String. The Object class’s toString method is normally overridden by a subclass.
- When an object is output using the %s format specifier, the object’s toString method is called implicitly to obtain its String representation.

### Section 9.5 Constructors in Subclasses

- The first task of a subclass constructor is to call its direct superclass’s constructor (p. 377) to ensure that the instance variables inherited from the superclass are initialized.

### Section 9.6 Software Engineering with Inheritance

- Declaring instance variables private, while providing non-private methods to manipulate and perform validation, helps enforce good software engineering.

### Section 9.7 Object Class

- See the table of class Object’s methods in Fig. 9.12.

## Self-Review Exercises

9.1 Fill in the blanks in each of the following statements:

- a) ______ is a form of software reusability in which new classes acquire the members of existing classes and embellish those classes with new capabilities.
- b) A superclass’s ______ members can be accessed in the superclass declaration and in subclass declarations.
- c) In a(n) ______ relationship, an object of a subclass can also be treated as an object of its superclass.
- d) In a(n) ______ relationship, a class object has references to objects of other classes as members.
- e) In single inheritance, a class exists in a(n) ______ relationship with its subclasses.
- f) A superclass’s ______ members are accessible anywhere that the program has a reference to an object of that superclass or to an object of one of its subclasses.
- g) When an object of a subclass is instantiated, a superclass ______ is called implicitly or explicitly.
