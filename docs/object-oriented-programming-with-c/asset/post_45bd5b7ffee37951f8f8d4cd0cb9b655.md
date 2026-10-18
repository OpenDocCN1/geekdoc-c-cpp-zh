
- An error caused by a program trying to access memory outside its address space. Caused by dereferencing a bad pointer.
- An object which performs operations according to the client’s requests but may not act upon other objects. It may only send messages to other objects as a result of a request from them, unless it is also a client of other servers. See Client.
- A digit that must be kept to preserve a given accuracy.
- The situation in which a derived class has only one base class.
- Symbolic coding in its original form before it is translated by a computer.
- A file containing source code.
- An area of memory used to hold a list of data and instructions on a temporary basis.
- An error caused by a program using too much temporary space (stack space) for its variables. Caused by a big program or by infinite recursion.
- See temporary variable.
- The opposite of dynamic binding. The functions are bound to the code to be executed at compile time. It is also known as *early binding*.
- A class member designated as static. A static data member declares a class variable - a variable associated with the class itself rather than with any instance of the class.
- An attribute of a variable definition that controls how the variable will be stored in memory.
- A source from which input data can be obtained or a destination to which output data can be sent.
- In object-oriented analysis, this is a linked set of
- A name that refers to a value. The data represented by the variable name can, at different times during the execution of a program, assume different values.
- The symbolic name given to a section of memory used to store a variable.
- A base class that has been qualified as virtual in the inheritance definition. In multiple inheritance, a derived class can inherit the members of a base class via two or more inheritance paths. If the base class is not virtual, the derived class will inherit more than one copy of the members of the base class. For a virtual base class, however, only one copy of its members will be inherited regardless of the number of inheritance paths between the base class and the derived class.
- A function qualified by the **virtual** keyword. When a virtual function is called via a pointer, the class of the object pointed to determines which function definition will be used. Virtual functions implement polymorphism, whereby objects belonging to different classes can respond to the same message in different ways.
- The ability of one object to be a server to others.
- A data type in C++. When used as a parameter in a function call, it indicates there is no return value. `void*` indicates that a generic pointer value is returned. When used in casts, it indicates that a given value is to be discarded.
- A graphical partition of screen for user interface.

## C++ Proficiency Test with Answers

### True/False

- 1. Just like virtual functions, we can also define virtual constructors in C++.
- 2. It is the job of the constructor to create vtable for virtual functions.
- 3. A copy constructor is called when an object is created on the basis of another object of the same class or when the compiler creates a temporary object.
- 4. If we do not mention an explicit access specifier for certain members of a class, then they will become public by default.
- 5. A class can be termed as an abstract class if it has at least one pure virtual function.
- 6. Function overloading is another name for function overriding.
- 7. If required, a copy constructor can be made to accept the object itself instead of the usual object reference.
- 8. The order in which constructors and destructors are called in an inheritance hierarchy is same i.e., base class first and then the subclasses.
- 9. We can use pointer to the base class object to call methods of the derived class.
- 10. We do not need to overload the assignment (=) operator to assign one object to another object of the same class; this functionality is provided by default in C++.
- 11. We can overload a function on the basis of passed value or passed reference.
- 12. Run time type identification should be avoided due to its associated performance overheads.
- 13. A friend function is allowed to directly access the private data members of the corresponding class object.
- 14. We can increase or decrease the size of an existing string by using the `resize()` function of the `string` class.
- 15. Just like friend function, it is also possible to make an entire class a friend of another class.
- 16. The shallow-copied member pointer points to the same memory location as the one pointed by the source member while the deep-copied pointer member points to a distinct memory location containing same value as the one pointed by the source member.
- 17. Even though `this` pointer appears to be a const pointer, we can make it point to some other object.
- 18. We can overload the `[]` operator to facilitate direct access to a privately declared one-dimensional array.
- 19. The `<<` operator is used to extract values from the stream while the `>>` operator is used to put values into the stream.
- 20. The `goodbit` flag of the `ios_base` class indicates everything is all right while the `badbit` flag indicates the occurrence of a nonfatal error.
- 21. The following code will compile successfully:

  ```cpp
  int num=10;
  class num
  {
  };
  int main()
  {
  class num num1;
  cout<<"Success";
  return 0;
  }
  ```

### Fill in the Blanks

- 12. To make the data members of a constant object modifiable we must declare such data members with ________________ storage class specifier.
- 13. The built-in function ________________ is used to check whether the argument character is a graphical i.e., printable and not a white space.
- 14. The ________________ handler may be used in situations where the type of the exceptions that may be thrown is not known.
- 15. The process of individually copying each member of an object to the corresponding members of another object (of same class) is known as ________________ copying.
- 16. The ________________ new operator is used to place the new entity being created at a specific pre-allocated memory location.
- 17. The ________________ pointer can be used to point to objects of varied types.
- 18. The ________________ pointer is used in C++ to implicitly bind a member function call with the calling object.
- 19. The overloading of ________________ operator does not pose any limitation on the number and type of associated operator parameters.
- 20. The implementation of function pointers is an instance of ________________ binding.
- 21. The scope resolution operator is represented by ________________.
- 22. The process of determining the dynamic type of an object at runtime is called ________________.
- 23. ________________ object of a class indicates that the real object of the class does not exist.
- 24. `wistream` and `wostream` are examples of ________________ character-based classes.
- 25. The __________ function is used to read and discard characters from an input stream.

### Multiple Choice Questions

- 1. Which of the following operators cannot be overloaded?
  - a. `^`
  - b. `==`
  - c. `.`
  - d. `!`

- 2. Which of the following return value of the **main** function signifies successful termination of a C++ program?
  - a. -1
  - b. 0
  - c. 1
  - d. None of the above

- 3. Which of the following is not a correct C++ comment?
  - a. `/*comment*/`
  - b. `//*comment*/`
  - c. `/*xx*\`
  - d. `/*//comment/*/`

- 4. Which of the following statements are not true about **wait()** and **delay()** functions?
  - a. Functionally, both are same; wait() is used in Linux/UNIX platforms while delay() is used in DOS/Windows platform.
  - b. Functionally, both are same; delay() is used in Linux/UNIX platforms while wait() is used in DOS/Windows platform.
  - c. wait(2) and delay(2) will result in a delay of two seconds.
  - d. wait(2) and delay(2000) will result in a delay of two seconds.

- 5. Which of the following will result in compiler error?
  - a. `cout << "Output string…" << 'endl';`
  - b. `cout << "Output string..." << endl;`
