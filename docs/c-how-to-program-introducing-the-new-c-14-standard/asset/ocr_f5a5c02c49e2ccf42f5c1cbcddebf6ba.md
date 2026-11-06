# *Section 9.10 Default Memberwise Assignment*

+   - The assignment operator (=) can be used to assign an object to another object of the same type. By default, such assignment is performed by **memberwise assignment** (p. 411).
+   - Objects may be passed by value to or returned by value from functions. C++ creates a new object and uses a **copy constructor** (p. 413) to copy the original object’s values into the new object.
+   - For each class, the compiler provides a default copy constructor that copies each member of the original object into the corresponding member of the new object.