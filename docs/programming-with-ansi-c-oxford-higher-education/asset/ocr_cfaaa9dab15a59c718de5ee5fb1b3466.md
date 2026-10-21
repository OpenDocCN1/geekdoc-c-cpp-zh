also shows how one can define PossibleSolutions() as a pure virtual function as all classes inherited from it must define it. The Error class (the base class) must also have generic solutions using PossibleSolutions() and, so, must have a body. As explained earlier, the body is defined outside the Error class.

# Calling a pure virtual function

If the PossibleSolutions() function of any class is called, it will call the PossibleSolutions() function for only that case. For example, consider the following statements:

```
Error *pError = new InitializationError;
pError->PossibleSolutions();

Error *qError = new LinkerError;
qError->PossibleSolutions();
```

This code will only display the possible solutions for initialization errors and linker errors. The need here is that it should also display errors related to their base classes. In case of initialization errors, it should also display the possible solutions for logical errors as well as general errors. In case of linker error, it should display possible solutions for linker errors, syntax errors, and general errors.

# Need for static invocation

This can be achieved by statically invoking PossibleSolutions() function for all the base classes, such as the PossibleSolutions() function of LinkerError in turn calls syntax as well as generic errors.

It can be seen that the function contains a call to the PossibleSolutions() function of the SyntaxError class, which in turn calls the Error::PossibleSolutions(); thus, one can get all possible solutions related to the error.

SyntaxError::PossibleSolutions() and Error::PossibleSolutions() are calls to virtual functions. They are different though. They are known as statically invoked calls to virtual functions.

Why is the static invocation needed? A linker error is also a syntax error, which in turn is an error. We need to print the description given by every class. Why a pure virtual function? We want programmers to implement PossibleSolutions() for every error that is a part of the hierarchy.

# RECAPITULATION

+   • Run-time polymorphism is an important feature of OO programming.
+   • C++ achieves run-time polymorphism using virtual functions.
+   • Run-time polymorphism adds overhead to the run-time system. Thus, it is not made a default. We have run-time polymorphism only when a function is defined as virtual.
+   • Run-time polymorphism is different from compile time polymorphism.
+   • In the case of a normal function being overloaded by the derived class, a base class pointer will always execute

+   • the function defined in the base class irrespective of where it is pointing to.
+   • The pointer, if pointing to a derived class object, executes a derived class function; otherwise, it executes the base class function.
+   • When a base class pointer is made to point to a derived class object, it can access only the base class subobject buried within the derived class object.
+   • Whenever a function is defined as virtual, a special pointer is embedded in every object. This pointer points to a table consisting of pointers to virtual functions that the object is capable of invoking.