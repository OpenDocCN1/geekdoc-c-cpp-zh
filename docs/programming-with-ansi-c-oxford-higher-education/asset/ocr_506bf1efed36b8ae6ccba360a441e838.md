that it is an error. Thus, the programmer has no control on how the structure and function interact.

In C++, it is possible to write a member function that is known only to that class, and the rest of the program is not aware of it. There is no direct way to call that member function using objects of other classes. Thus, the objects of class Student can call StudentPrintDetails, but the objects of class dog cannot call this function. This is one of the fundamental differences between C and C++. Thus, we can write Lara.PrintDetails() but we cannot write Snoopy.PrintDetails(). It should be noted that member functions are called using dot notation similar to other data elements. The functions now belong to the class.

The definition of a class is similar to the C struct, as we have mentioned earlier. We can define class Student and can have, say, Student_1 as an object of type Student. If we define class Teacher and then define Bob as a variable of type Teacher, Teacher is a class where Bob is an object.

# 1.3.1 Object-oriented View of Classes and Objects

We will now take a different look at classes and objects, from the object-oriented point of view. The entities involved in the discussion in the previous sections are implemented in a C++ program as a class. The class is a representation of the real-world entity (e.g., a teacher or a student) or an entity added by a programmer for convenience (e.g., the roll call object) with respective attributes that are required to solve the problem at hand. It can be seen that this description is quite vague. For a given problem, the set of entities that the author has chosen probably is different from that chosen by the readers. The same problem is being solved but handled differently. Moreover, the attributes that the author has chosen probably are very different from that of the readers, even if both are solving the same problem.

All entities that are modelled in the program are implemented as classes. Thus, the classes in one program could be different from that in another when solving the same problem. Such classes (Teacher, Student, or RollCall) do not refer to an individual entity, but we refer to them in general. The entities such as Ganesh as a student, Mathew as a teacher, or roll call 16030903 (roll call created on 16 03 09 and of the third lecture) are instances of the generic entities that we have discussed so far. In object-oriented parlance, they are known as objects. Objects are variables of type class and can be defined similar to variables. Assuming that the classes Student, Teacher, and RollCall exist, the following are valid C++ statements, which define the individual entities or objects for respective classes:

```
Student Ganesh;
Teacher Mathew;
RollCall RollCall16030903;
```

In these definitions, the left-hand side (LHS) part is the data type and the right-hand side (RHS) part is the variable. Once the classes have been defined, the class name can indeed be used as a data type. So, in this case, the classes are Student, Teacher, and RollCall. The instances of these classes are Ganesh, Mathew, and RollCall16030903, which are also called the objects of the respective classes. The classes are sometimes referred to as user-defined data types compared to built-in data types, such as int and char. Thus, in our example, Teacher, Student, and RollCall are also called user-defined data types.