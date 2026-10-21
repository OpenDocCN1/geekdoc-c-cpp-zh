```
{
    clrscr();
    first *f=new second;
    delete f;
    getch();
}
```

OUTPUT :
Second des called
First des called

EXPLANATION : In the main we have declared a pointer of type first and in the pointer we have stored address of an object of class second. When delete ptr executes, destructor of second class is called first then destructor of first class is called. This is just because of virtual. If it were not in the first class only the destructor of first class would have been called and ptr wouldn't be deleted. So this is the main use of virtual destructor where you have pointer of base class and object stored is of derived class.

## 10.11 PONDERABLE POINTS

+   1. A pointer of base class can store address of an object of derived class but reverse is not true.
+   2. This pointer is a constant pointer which stores the address of the current object.
+   3. This pointer can only be used inside the non-static member functions of the class.
+   4. In the absence of virtual keyword, pointer of base class will call only its function no matter address of what type of object is stored inside the pointer.
+   5. When virtual function is present then function call is made by checking the contents of pointer rather then checking type of pointer.
+   6. For every class in which virtual function is present and all other classes derived from this class, VTABLE is created.
+   7. The VTABLE contains addresses of all the virtual function present/inherited in the class. A special pointer vptr points to the VTABLE.
+   8. A pure virtual function is a function which has no body.
+   9. For a class to be abstract class, it must have at least one pure virtual function.
+   10. Pointers and references of an abstract class can be created.
+   11. Virtual function is the only mechanism to provide-run-time polymorphism in C++.
+   12. Binding is the linking of function call with the place where function definition is written.
+   13. When binding is done at compile time it is known as early-binding, compile time binding or static binding.
+   14. When binding is done at run time it is known as late-binding, runtime binding or dynamic binding.
+   15. Static binding provides efficiency but less flexible.
+   16. Dynamic binding provides flexibility but less efficient.

## EXERCISE

+   **A. True and False:**
+   
+   1. An abstract class can be instantiated.
+   2. This pointer points to current object only.
+   3. A class containing at least one pure virtual function is known as abstract class.
+   4. A class whose objects cannot be created is known as abstract class.
+   5. All functions in an abstract base class must be declared as abstract class.
+   6. Virtual function cannot be overloaded.
+   7. Polymorphism can be implemented only using virtual functions.

+   **B. Answer the Following Questions:**
+   
+   1. How do create pointer to objects of a class?
+   2. How can be call member function of a derived class when pointer is of base class and virtual keyword is not present?
+   3. What is virtual function?
+   4. What is VTABLE?
+   5. How does virtual function works?
+   6. What is this pointer? What are its main characteristics?
+   7. How do we implement run-time polymorphism in C++?
+   8. What is binding? What is the significance of binding?
+   9. What is an abstract class?
+   10. What is pure virtual function? How it is different from all other functions?
+   11. Why cannot we create an object of an abstract class?
+   12. What is object slicing?
+   13. What is the significance of virtual destructor?
+   14. Why cannot we have virtual destructor?
+   15. Can we call virtual function explicitly without using pointers?

+   **C. Brain Drill:**
+   
+   1. Suppose that there is an abstract class ‘Shape’, which is the base class of classes ‘Polygon’ and ‘Circle’. “Polygon” class is the base class from which a class Rectangular is derived. Pure virtual functions compute Area and compute Perimeter are declared in the class Shape. These functions are actually defined in the derived classes “Rectangle” and “Circle”. Define the classes “Shape”, “Polygon”, “Rectangle” and “Circle”. Write a global function “ComputeAllArea” as double computeAllArea(Shape*s[100], int numberofShapes).

The above function computes the total area of all shapes object pointed to by s[0], s[1], …s[numberOfShapes].

2. Suppose that you need to define classes for employee and manager objects. An employee has a name, an employee code, salary and age. A manager is also an employee. But a manager object contains an additional list of references to employee objects that the manager supervises. An employee object should also contain a reference to his/her manager. A manager can supervises at most 10 employee. It is required to print details of employee or a manager. When information of an employee object is printed, his/her name, salary and age is printed. When information of a manager object is printed, his/her name, salary and age is printed and names of all the employees that he/she supervises are displayed. Define the classes keeping the following in mind:

+   (a) References to employee objects can be added/deleted from the list of supervised employees in a manager object.
+   
+   (b) Reference to the manager object can be modified for an employee object.

## INPUT-OUTPUT AND MANIPULATORS IN C++

### 11.1 INTRODUCTION

In all the earlier chapters, we have worked with cin and cout for taking all different types of data as input and displaying them. But, we have not worked with the formatted output i.e., the way we want to print the data onto screen. For managing the input and output operations C++ provides the concept of stream classes. We know that cin is treated as standard input stream and cout as standard output stream classes. We known that cin is treated as standard input streams and cout as standard output streams. A stream is termed as input stream and when data is sent by the program to the output device say screen, the stream termed as output stream. It is quite obvious as we have seen in almost all the C++ programs so far that to take data from keyboard we have cin, which receives data and display s onto the screen. Thus, cin is standard input stream and cout is standard output stream.

We have also said that >> is an extraction operator << is insertion operator. This is so as cin >> extraction data from input stream from input stream and cout << displays inserts data into output stream. C++ provides numbers of stream classes for the efficient handling input and output and which is our next topic of discussion.

### 11.2 C++ STREAM CLASSES

In C++ there are number of streams classes for defining various streams related with files and for doing input output operations. All these classes are defined in the file iostream.h. Figure given below shows the hierarchy of these classes :

![](img/ad5299318df8d4d7c6df5eaa86590ea3_531_0.png)

Figure 11.1. Hierarchy of ios file

As can be seen from the figure that :

+   1. **ios** class is the topmost class in the **stream** classes hierarchy. It is the base class for **istream, ostream and streambuf** class.
+   2. **istream, ostream** serves the base classes for **iostream class**. The class **istream** is used for input and **ostream** for output.
+   3. Class **ios** is indirectly to **iostream** class using **istream** and **ostream**. To avoid the duplicity of data and member functions of **ios** class, it is declared as virtual **base class** when inheriting **in istream and ostream** as :

```
class istream : virtual public ios
{
};

class ostream :virtual public ios
{
};
```

4. The _withassign classes are provided with extra functionality for the assignment operations that's why _withassign classes.
After discussing about various stream classes we now understand their purpose and what type of facilities are provided by these stream classes.

# 1. The ios Class

The ios class is responsible for providing all input and output facilities to all other stream classes as it is the topmost class in the hierarchy of stream classes. As we will be seeing later in the chapter, this class provides number of functions for efficient handling of formatted output for strings and numbers.

# 2. The istream Class

This class is responsible for handling input stream. It provides number of functions for handling chars, strings and objects, record etc, besides inheriting the properties from ios class. The istream class provides the basic capability for sequential and random—access input. An istream
