# Including the Base-Class Header in the Derived-Class Header

Notice that we #include the base class’s header in the derived class’s header (Fig. 10.4, line 6). This is necessary for several reasons:

+   - For the derived class to inherit from the base class in line 8 (Fig. 10.4), the compiler requires the base-class definition from `SalariedEmployee.h`.
+   - **The compiler determines an object’s size from its class’s definition**, so it must know the class definition to reserve the proper amount of memory for a new object. **A derived-class object’s size depends on the data members declared explicitly in its class definition and the data members inherited from its direct and indirect base classes.**⁷ Including the base class’s definition allows the compiler to determine the complete memory requirements for all the data members that contribute to a derived-class object’s total size.
+   - The base-class definition also enables the compiler to determine whether the derived class uses the base class’s inherited members properly. For example, **the compiler uses the base class’s function prototypes to validate derived-class function calls to inherited base-class functions.**

# Eliminating Repeated Code via Implementation Inheritance

With implementation inheritance, the base class declares the common data members and member functions of all the classes in the hierarchy. When changes are required for these common features, you make the changes only in the base class. The derived classes then inherit the changes and must be recompiled. Without inheritance, changes would need to be made to all the source-code files that contain a copy of the code in question.⁸

![](bbox=[0.138, 0.544, 0.176, 0.573])

# Checkpoint

+   1. *(Fill-in)* A derived-class constructor can call its base-class’s constructor via a(n) ______—a member initializer that passes arguments to a base-class constructor. **Answer:** base-class initializer.
+   2. *(Code)* Assume class `SalariedEmployee` has a `print` member function that takes no arguments. Also, assume class `SalariedCommissionEmployee` inherits from `SalariedEmployee` and redefines `print`. Write an expression that would call `SalariedEmployee`’s `print` function from `SalariedCommissionEmployee`’s `print` function. **Answer:** `SalariedEmployee::print()`
+   3. *(True/False)* C++ rigidly enforces restrictions on accessing private data members. Even a derived class, which is intimately related to its base class, cannot directly access its base class’s private data. **Answer:** True.

+   7. All objects of a class share one copy of the class’s member functions, which are stored separately from those objects and are not part of their size.
+   8. Again, the downside of implementation inheritance, especially in deep inheritance hierarchies, is that it creates a tight coupling among the hierarchy’s classes, making it difficult to modify.