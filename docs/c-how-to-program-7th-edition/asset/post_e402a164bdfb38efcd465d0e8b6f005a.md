
When deleting a derived-class object through a base-class pointer, the destructor for the appropriate class is called. After a derived-class destructor runs, the destructors for all of that class's base classes run all the way up the hierarchy.

### Terminology

- abstract base classes 593
- abstract classes 593
- concrete classes 593
- displacement into a *vtable* 615
- downcasting 586
- dynamic binding 587
- dynamic casting 574
- dynamic_cast 619
- implementation inheritance 596
- interface inheritance 596
- iterator class 595
- late binding 587
- name function of class type_info 619
- nonvirtual destructor 620
- offset into a *vtable* 615
- override 586
- polymorphism 573
- pure specifier (with virtual functions) 594
- pure virtual function 594
- runtime type information (RTTI) 574
- static binding 587
- typeid operator 619
- type_info class 619
- `<typeinfo>` header file 619
- virtual destructor 620
- virtual function 586
- virtual function table (*vtable*) 613

### Self-Review Exercises

- 13.1 Fill in the blanks in each of the following statements:
  - a) Treating a base-class object as a(n) ______ can cause errors.
  - b) Polymorphism helps eliminate ______ logic.
  - c) If a class contains at least one pure virtual function, it's a(n) ______ class.
  - d) Classes from which objects can be instantiated are called ______ classes.
  - e) Operator ______ can be used to downcast base-class pointers safely.
  - f) Operator typeid returns a reference to a(n) ______ object.
  - g) ______ involves using a base-class pointer or reference to invoke virtual functions on base-class and derived-class objects.
  - h) Overridable functions are declared using keyword ______.
  - i) Casting a base-class pointer to a derived-class pointer is called ______.

- 13.2 State whether each of the following is true or false. If false, explain why.
  - a) All virtual functions in an abstract base class must be declared as pure virtual functions.
  - b) Referring to a derived-class object with a base-class handle is dangerous.
  - c) A class is made abstract by declaring that class virtual.
  - d) If a base class declares a pure virtual function, a derived class must implement that function to become a concrete class.
  - e) Polymorphic programming can eliminate the need for switch logic.

### Answers to Self-Review Exercises

- 13.1 a) derived-class object. b) switch. c) abstract. d) concrete. e) dynamic_cast. f) type_info.
  g) Polymorphism. h) virtual. i) downcasting.

13.2 a) False. An abstract base class can include virtual functions with implementations. b) False. Referring to a base-class object with a derived-class handle is dangerous. c) False. Classes are never declared virtual. Rather, a class is made abstract by including at least one pure virtual function in the class. d) True. e) True.

### Exercises

13.3 How is it that polymorphism enables you to program “in the general” rather than “in the specific”? Discuss the key advantages of programming “in the general.”

13.4 Discuss the problems of programming with switch logic. Explain why polymorphism can be an effective alternative to using switch logic.

13.5 Distinguish between inheriting interface and inheriting implementation. How do inheritance hierarchies designed for inheriting interface differ from those designed for inheriting implementation?

13.6 What are virtual functions? Describe a circumstance in which virtual functions would be appropriate.

13.7 Distinguish between static binding and dynamic binding. Explain the use of virtual functions and the vtable in dynamic binding.

13.8 Distinguish between virtual functions and pure virtual functions.

13.9 (*Abstract Base Classes*) Suggest one or more levels of abstract base classes for the Shape hierarchy discussed in this chapter and shown in Fig. 12.3. (The first level is Shape, and the second level consists of the classes TwoDimensionalShape and ThreeDimensionalShape.)

13.10 How does polymorphism promote extensibility?

13.11 You've been asked to develop a flight simulator that will have elaborate graphical outputs. Explain why polymorphic programming could be especially effective for a problem of this nature.

13.12 (*Payroll System Modification*) Modify the payroll system of Figs. 13.13–13.23 to include private data member birthDate in class Employee. Use class Date from Figs. 11.9–11.10 to represent an employee's birthday. Assume that payroll is processed once per month. Create a vector of Employee references to store the various employee objects. In a loop, calculate the payroll for each Employee (polymorphically), and add a $100.00 bonus to the person's payroll amount if the current month is the month in which the Employee's birthday occurs.

13.13 (*Shape Hierarchy*) Implement the Shape hierarchy designed in Exercise 12.7 (which is based on the hierarchy in Fig. 12.3). Each TwoDimensionalShape should contain function getArea to calculate the area of the two-dimensional shape. Each ThreeDimensionalShape should have member functions getArea and getVolume to calculate the surface area and volume, respectively, of the three-dimensional shape. Create a program that uses a vector of Shape pointers to objects of each concrete class in the hierarchy. The program should print the object to which each vector element points. Also, in the loop that processes all the shapes in the vector, determine whether each shape is a TwoDimensionalShape or a ThreeDimensionalShape. If a shape is a TwoDimensionalShape, display its area. If a shape is a ThreeDimensionalShape, display its area and volume.

13.14 (*Project: Polymorphic Screen Manager Using Shape Hierarchy*) Develop a basic graphics package. Use the Shape hierarchy implemented in Exercise 13.13. Limit yourself to two-dimensional shapes such as squares, rectangles, triangles and circles. Interact with the user. Let the user specify the position, size, shape and fill characters to be used in drawing each shape. The user can specify more than one of the same shape. As you create each shape, place a Shape* pointer to each new Shape object into an array. Each Shape class should now have its own draw member function. Write a polymorphic screen manager that walks through the array, sending draw messages to each object in the array to form a screen image. Redraw the screen image each time the user specifies an additional shape.

13.15 (*Package Inheritance Hierarchy*) Use the Package inheritance hierarchy created in Exercise 12.9 to create a program that displays the address information and calculates the shipping costs for several Packages. The program should contain a vector of Package pointers to objects of

## 14 Templates

> Behind that outside pattern the dim shapes get clearer every day.
> It is always the same shape, only very numerous.
>
> —Charlotte Perkins Gilman

> Every man of genius sees the world at a different angle from his fellow.
>
> —Havelock Ellis

> ...our special individuality, as distinguished from our generic humanity.
>
> —Oliver Wendell Holmes, Sr

### Objectives

In this chapter you'll learn:

- To use function templates to conveniently create a group of related (overloaded) functions.
- To distinguish between function templates and function-template specializations.
- To use class templates to create groups of related types.
- To distinguish between class templates and class-template specializations.
- To overload function templates.
- To understand the relationships among templates, friends, inheritance and static members.

![](img/023f159fdd47d944d48e08843cea732d_662_0.png)

### 14.2 Function Templates

Overloaded functions normally perform similar or identical operations on different types of data. If the operations are identical for each type, they can be expressed more compactly and conveniently using function templates. Initially, you write a single function-template definition. Based on the argument types provided explicitly or inferred from calls to this function, the compiler generates separate source-code functions (i.e., function-template specializations) to handle each function call appropriately. In C, this task can be performed using macros created with the preprocessor directive #define (see Appendix E, Preprocessor). However, macros can have serious side effects and do not enable the compiler to perform type checking. Function templates provide a compact solution, like macros, but enable full type checking.

> **Error-Prevention Tip 14.1**
>
> *Function templates, like macros, enable software reuse. Unlike macros, function templates help eliminate many types of errors through the scrutiny of full C++ type checking.*

All function-template definitions begin with keyword template followed by a list of template parameters to the function template enclosed in angle brackets (< and >); each template parameter that represents a type must be preceded by either of the interchangeable keywords class or typename, as in

```cpp
template< typename T >
```

or

```cpp
template< class ElementType >
```

or

```cpp
template< typename BorderType, typename FillType >
```

The type template parameters of a function-template definition are used to specify the types of the arguments to the function, to specify the return type of the function and to declare variables within the function. The function definition follows and appears like any other function definition. Keywords typename and class used to specify function-template parameters actually mean “any fundamental type or user-defined type.”

> **Common Programming Error 14.1**
>
> *Not placing keyword class or keyword typename before each type template parameter of a function template is a syntax error.*

**Example: Function Template printArray**

Let’s examine function template printArray in Fig. 14.1, lines 7–14. Function template printArray declares (line 7) a single template parameter T (T can be any valid identifier) for the type of the array to be printed by function printArray; T is referred to as a type template parameter, or type parameter. You’ll see nontype template parameters in Section 14.5.
