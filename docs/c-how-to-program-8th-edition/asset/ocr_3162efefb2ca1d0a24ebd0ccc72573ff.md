+   - When deriving a class from a public base class (p. 502), public members of the base class become public members of the derived class, and protected members of the base class become protected members of the derived class.
+   - When deriving a class from a protected base class (p. 502), public and protected members of the base class become protected members of the derived class.
+   - When deriving a class from a private base class (p. 502), public and protected members of the base class become private members of the derived class.

# Self-Review Exercises

+   **I2.1** Fill in the blanks in each of the following statements:
+   
+   a) ________ is a form of software reuse in which new classes absorb the data and behaviors of existing classes and embellish these classes with new capabilities.
+   
+   b) A base class’s ________ members can be accessed in the base-class definition, in derived-class definitions and in friends of the base class its derived classes.
+   
+   c) In a(n) ________ relationship, an object of a derived class also can be treated as an object of its base class.
+   
+   d) In a(n) ________ relationship, a class object has one or more objects of other classes as members.
+   
+   e) In single inheritance, a class exists in a(n) ________ relationship with its derived classes.
+   
+   f) A base class’s ________ members are accessible within that base class and anywhere that the program has a handle to an object of that class or one of its derived classes.
+   
+   g) A base class’s protected access members have a level of protection between those of public and ________ access.
+   
+   h) C++ provides for ________, which allows a derived class to inherit from many base classes, even if the base classes are unrelated.
+   
+   i) When an object of a derived class is instantiated, the base class’s ________ is called implicitly or explicitly to do any necessary initialization of the base-class data members in the derived-class object.
+   
+   j) When deriving a class from a base class with public inheritance, public members of the base class become ________ members of the derived class, and protected members of the base class become ________ members of the derived class.
+   
+   k) When deriving a class from a base class with protected inheritance, public members of the base class become ________ members of the derived class, and protected members of the base class become ________ members of the derived class.

+   **I2.2** State whether each of the following is *true* or *false*. If *false*, explain why.
+   
+   a) Base-class constructors are not inherited by derived classes.
+   
+   b) A *has-a* relationship is implemented via inheritance.
+   
+   c) A car has an *is-a* relationship with the Steeringwheel and Brakes classes.
+   
+   d) Inheritance encourages the reuse of proven high-quality software.
+   
+   e) When a derived-class object is destroyed, the destructors are called in the reverse order of the constructors.

# Answers to Self-Review Exercises

**I2.1** a) Inheritance.  b) protected.  c) *is-a* or inheritance (for public inheritance).  d) *has-a* or composition or aggregation.  e) hierarchical.  f) public.  g) private.  h) multiple inheritance.  i) constructor.  j) public, protected.  k) protected, protected.

**I2.2** a) True.  b) False. A *has-a* relationship is implemented via composition. An *is-a* relationship is implemented via inheritance.  c) False. This is an example of a *has-a* relationship. Class Car has an *is-a* relationship with class Vehicle.  d) True.  e) True.