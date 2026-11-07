in the GradeBook object to a shorter name that does not need to be truncated. Then, lines 25–28 output the course names for the GradeBook objects again.

# Additional Notes on Set Functions

A public set function such as setCourseName should carefully scrutinize any attempt to modify the value of a data member (e.g., courseName) to ensure that the new value is appropriate for that data item. For example, an attempt to set the day of the month to 37 should be rejected, an attempt to set a person’s weight to zero or a negative value should be rejected, an attempt to set a grade on an exam to 185 (when the proper range is zero to 100) should be rejected, and so on.

![](bbox=[0.131, 0.296, 0.19, 0.338])

> **Software Engineering Observation 3.3**  
> _Making data members private and controlling access, especially write access, to those data members through public member functions helps ensure data integrity._

![](bbox=[0.131, 0.368, 0.19, 0.41])

> **Error-Prevention Tip 3.4**  
> _The benefits of data integrity are not automatic simply because data members are made private—you must provide appropriate validity checking and report the errors._

A set function could return a value indicating that an attempt was made to assign invalid data to an object of the class. A client could then test the return value of the set function to determine whether the attempt to modify the object was successful and to take appropriate action if not. We will do that in later chapters after we introduce a bit more programming technology. In C++, clients of objects also can be notified of problems via the _exception-handling mechanism_, which we begin discussing in Chapter 7 and present in-depth in Chapter 17.

# 3.9 Wrap-Up

In this chapter, you created user-defined classes, and created and used objects of those classes. We declared data members of a class to maintain data for each object of the class. We also defined member functions that operate on that data. You learned that member functions that do not modify a class’s data should be declared const. We showed how to call an object’s member functions to request the services the object provides and how to pass data to those member functions as arguments. We discussed the difference between a local variable of a member function and a data member of a class. We also showed how to use a constructor and a member-initializer list to ensure that every object is initialized properly. You learned that a single-parameter constructor should be declared explicit, and that a constructor cannot be declared const because it modifies the object being initialized. We demonstrated how to separate the interface of a class from its implementation to promote good software engineering. You learned that using directives and using declarations should never be placed in headers. We presented a diagram that shows the files that class-implementation programmers and client-code programmers need to compile the code they write. We demonstrated how set functions can be used to validate an object’s data and ensure that objects are maintained in a consistent state. UML class diagrams were used to model classes and their constructors, member functions and data members. In the next chapter, we begin our introduction to control statements, which specify the order in which a function’s actions are performed.