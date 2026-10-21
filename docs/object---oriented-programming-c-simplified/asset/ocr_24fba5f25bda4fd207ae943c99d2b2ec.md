# Object-Oriented Programming C++ Simplified

With the help of containership we can only use public data member/ function of the class but not protected or private. In the first class we have returned the reference with the help of getnum function. In the default constructor of class second we assign value of 200 to num of first class by calling the function getnum. Then we show if by c call to show.



+   1. Inheritance is the mechanism of deriving new class from an existing class. The old class and new class is known as in pair : super-sub, base-derived, parent-child.
+   
+   2. In inheritance provides the idea of reusability. Code once written can be used again and again in several different classes.
+   
+   3. C++ provides support for : single level and multilevel inheritance, multiple inheritance, hierarchical inheritance, hybrid inheritance.
+   
+   4. Private member are never inherited.
+   
+   5. Virtual base class is used to avoid dupicity of data members into the target derived class.
+   
+   6. In an inheritance hierarchy constructor of base class is called first, then constructor of derived class is called.
+   
+   7. In an inheritance hierarchy destructor class is called first, then destructor of base class is called.
+   
+   8. Containership allows us to use object of one class as a member of other class. This type of containership provides the idea of has_a relationship or nesting of classes.

> EXERCISE



+   1. Public variables can be accessed from anywhere in the program.
+   
+   2. Inheritance helps in maintenance of code.
+   
+   3. A derived class is often called sub-class because it represents a subset of its base class.
+   
+   4. A pointer to base class can point to an object of a derived class of that base class.
+   
+   5. If no constructor is specified for a derived class, then object of derived class will use constructor in the base class.
+   
+   6. An object of derived class cannot access public members of the base class using dot operator.
+   
+   7. In multiple inheritances, all the constructors are invoked in the reverse of derivation and destructor are invoked in the same order.
+   
+   8. It is not possible to assign a base class pointer to a derived class object.
+   
+   9. Sub classes can access protected members of a base class but not private members.
+   
+   10. When name clash occurs in multiple inheritances, the ambiguity is resolved by using scope resolution operator.
+   
+   11. A function that is declared as a friend of a base class can be inherited by the derived class.
+   
+   12. Sub-classes can access private members of a parent class, but not protected members.