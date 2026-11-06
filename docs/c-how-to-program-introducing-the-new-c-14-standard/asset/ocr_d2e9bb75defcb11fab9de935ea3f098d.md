# Section 3.4.2 Initializing `Account` Objects  
When They’re Created

+   - When you create an object, C++ calls the class’s constructor to initialize that object. If a constructor has parameters, the corresponding arguments are placed in braces, `{` and `}`, to the right of the object’s variable name.
+   - When you create an object without placing braces to the right of the object’s variable name, C++ implicitly calls the class’s **default constructor** (p. 87).
+   - In any class that does not explicitly define a constructor, the compiler provides a default constructor (which always has no parameters).
+   - The default constructor does not initialize the class’s fundamental-type data members, but does call the default constructor for each data member that’s an object of another class.
+   - A `string`’s default constructor initializes the object to the empty `string`.
+   - An uninitialized fundamental-type variable contains an undefined (“garbage”) value.
+   - If a class defines a constructor, the compiler will not create a default constructor for that class.