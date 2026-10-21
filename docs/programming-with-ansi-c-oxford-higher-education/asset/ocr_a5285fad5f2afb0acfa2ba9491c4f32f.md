in the constructor. In such a case, it becomes imperative for the programmer to deallocate the memory when the object goes out of scope. Hence, the situation demands a destructor. Now, the normal assignment also does not work properly. The assigned object also needs dynamic memory allocation, and therefore, the assignment operator is also overloaded in that case.

# RECAPITULATION

+   - C++ has user-defined objects similar to the built-in data types.
+   - Constructor and destructors provide initialization and termination effects to user-defined objects similar to built-in data types.
+   - User-defined objects may need to initialize themselves when defined.
+   - Constructors are functions having the same name as class. They can be either default or parameterized.
+   - Single-argument constructor is a special one. The compiler automatically generates a conversion operator when such a constructor is defined.
+   - Explicit constructor avoids automatic generation of conversion operator.
+   - Whenever the user has not defined any constructor, C++ provides the effect of one. It may or may not physically synthesize a constructor depending on the situation.
+   - The compiler-provided destructor cannot do the job of a programmer. The programmer must initialize members using user-defined constructors in cases where the compiler-provided default constructor is not appropriate.
+   - It is possible to have multiple constructors for a single class. In this case, all the constructors must have either different numbers of arguments or different types of arguments.
+   - It is also possible to have default arguments to the constructor similar to a normal function.
+   - The objects can be dynamically initialized by explicitly calling a constructor function. It is also possible to have a constructor with dynamic allocation.
+   - A destructor is also to be defined and the assignment operator to be overloaded in most of the cases where a dynamic constructor is used.
+   - The assignment operator and the copy constructor are different. The copy constructor changes the behaviour of initialization whereas an assignment operator overloading changes the behaviour of the assignment.
+   - MIL is a better method for some cases and a must for constant, references and object members of the class.
+   - The order in which MIL is executed depends on the order of declaration of data members and not on the order in which MIL is specified.
+   - Destructors are needed to provide user-defined termination effects when the object goes out of scope.
+   - The lifetime of the object is after the construction function is executed and just before the destructor is executed.

# KEYWORDS

Constructor This is a function with the same name as the class itself and is responsible for constructing and returning the objects of the class.
Copy constructor An object is copied to another using initialization by executing the copy constructor.
Default constructor This is a constructor without any argument.
Default constructor provided by compiler This refers to the constructor that is provided by the compiler when the user has not defined any. It may not be physically synthesized by the compiler.
Destructor This is a function that bears the same name as the class itself and is preceded by ~. The destructor is automatically called when the object goes out of scope.
Dynamic initialization The initialization that happens at run-time is known as dynamic initialization.
Explicit constructor This is the single-argument constructor that is defined with the keyword explicit before