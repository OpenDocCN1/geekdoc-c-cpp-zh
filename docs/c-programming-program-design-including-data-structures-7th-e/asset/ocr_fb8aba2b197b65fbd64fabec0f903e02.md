+   10. If in the heading of the definition of a derived class’s constructor, no call to a constructor (with parameters) of a base class is specified, then during the derived class’s object declaration and initialization, the default constructor (if any) of the base class executes.
+   11. When initializing the object of a derived class, the constructor of the base class is executed first.
+   12. Review the inheritance rules given in this chapter.
+   13. In composition (aggregation), a member of a class is an object of another class.
+   14. In composition (aggregation), a call to the constructor of the member objects is specified in the heading of the definition of the class’s constructor.
+   15. The three basic principles of OOD are encapsulation, inheritance, and polymorphism.
+   16. An easy way to identify classes, objects, and operations is to describe the problem in English and then identify all of the nouns and verbs. Choose your classes (objects) from the list of nouns and your operations from the list of verbs.

# EXERCISES

The number in parentheses at the end of an exercise refers to the learning objective listed at the beginning of the chapter.

+   1. Mark the following statements as true or false.
+      a. In single inheritance, a base class can create only one derived class. (1)
+      b. The `public` members of a base class can only be inherited as `public` members in the derived class. (2)
+      c. To redefine (or override) a member function of the base class in the derived class, the corresponding member function must have the same name, number, and type of parameters. (3)
+      d. If the derived class does not override a `public` member function of the base class, you may specify a call to that `public` member function by using the name of the function and the appropriate parameter list. (3)
+      e. The constructor of a derived class can specify a call to the constructor of the base class in the heading of the function definition. (4)
+      f. The constructor of a derived class can specify a call to the constructor of the base class using the name of the class. (4)
+      g. Suppose that x and y are classes, one of the member variables of x is an object of type y, and both classes have constructors. The constructor of x specifies a call to the constructor of y by using the object name of type y. (4)
+      h. When the destructor of the derived class executes, it automatically invokes the destructor of the base class. (5)