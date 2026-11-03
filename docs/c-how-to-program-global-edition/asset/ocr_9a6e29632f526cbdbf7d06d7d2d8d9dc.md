# Section 20.7 (Optional) Polymorphism, Virtual Functions and Dynamic Binding "Under the Hood"

+   - Dynamic binding requires that at runtime, the call to a virtual member function be routed to the virtual function version appropriate for the class. A virtual function table called the vtable (p. 832) is implemented as an array containing function pointers. Each class with virtual functions has a vtable. For each virtual function in the class, the vtable has an entry containing a function pointer to the version of the virtual function to use for an object of that class. The virtual function to use for a particular class could be the function defined in that class, or it could be a function inherited either directly or indirectly from a base class higher in the hierarchy.
+   - When a base class provides a virtual member function, derived classes can override the virtual function, but they do not have to override it.
+   - Each object of a class with virtual functions contains a pointer to the vtable for that class. When a function call is made from a base-class pointer to a derived-class object, the appropriate function pointer in the vtable is obtained and dereferenced to complete the call at execution time.
+   - Any class that has one or more null ptr pointers in its vtable is an abstract class. Classes without any null ptr vtable pointers are concrete classes.
+   - New kinds of classes are regularly added to systems and accommodated by dynamic binding.

# Section 20.8 Case Study: Payroll System Using Polymorphism and Runtime Type Information with Downcasting, dynamic_cast, typeid and type_info

+   - Operator dynamic_cast (p. 836) checks the type of the object to which a pointer points, then determines whether the type has an is-a relationship with the type to which the pointer is being converted. If so, dynamic_cast returns the object's address. If not, dynamic_cast returns null ptr.
+   - Operator typeid (p. 838) returns a reference to a type_info object (p. 838) that contains information about the operand's type, including the type name. To use typeid, the program must include header <typeinfo> (p. 838).
+   - When invoked, type_info member function name (p. 838) returns a pointer-based string that contains the name of the type that the type_info object represents.
+   - Operators dynamic_cast and typeid are part of C++'s runtime type information (RTTI; p. 836) feature, which allows a program to determine an object's type at runtime.

# Self-Review Exercises

# 20.1 Fill in the blanks in each of the following statements:

+   a) Treating a base-class object as a(n) ______ can cause errors.
+   b) Polymorphism helps eliminate ______ logic.
+   c) If a class contains at least one pure virtual function, it's a(n) ______ class.
+   d) Classes from which objects can be instantiated are called ______ classes.
+   e) Operator ______ can be used to downcast base-class pointers safely.
+   f) Operator typeid returns a reference to a(n) ______ object.
+   g) ______ involves using a base-class pointer or reference to invoke virtual functions on base-class and derived-class objects.
+   h) Overridable functions are declared using keyword ______.
+   i) Casting a base-class pointer to a derived-class pointer is called ______.

# 20.2 State whether each of the following is true or false. If false, explain why.

+   a) All virtual functions in an abstract base class must be declared as pure virtual functions.
+   b) Referring to a derived-class object with a base-class handle is dangerous.
+   c) A class is made abstract by declaring that class virtual.