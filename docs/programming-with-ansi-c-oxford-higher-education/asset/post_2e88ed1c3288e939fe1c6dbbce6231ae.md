
C++ is almost a superset of C. Since the syntax of C++ is extended from C, knowledge of C is useful while learning C++.

defining struct Student, struct supplier, or struct customer containing names, addresses, etc.). This mapping is not complete. We can add attributes of an entity student in the struct type variable (e.g., name, address, and marks of respective subjects), but actions related to them (such as enrolment and getting result) cannot be stored within the structure. We usually write functions to perform such activities in C, but these functions are not part of the struct keyword; they are independent.

C++ introduces a new element called class, which is an extension to struct, and provides the facility to store actions in the form of functions within the entities themselves. It is similar to storing the Student object with all the data attributes such as name and address as well as action attributes such as enrolment, reading, and printing details of the concerned Student object. This process of combining data and function attributes of an entity is known as encapsulation.

> Note A C struct represents only a part of an entity, that is, data. An object represents an entity completely, that is, data as well as methods.

## 1.1.3 Object-based and Object-oriented Design

C++ is designed for providing both object-based and object-oriented programming. Before we look at the differences between the two, let us assume that the discussion that follows is applicable to both the cases.

It is not easy to provide object orientation in a computer language while maintaining acceptable efficiency levels. A major advantage of the C language is its efficiency. Programs written in C execute faster than if written in any other high-level language. The designers of C++ wanted the same efficiency level in C++ as in C.

The normal rule of thumb is that the more object-oriented the language, the slower the execution of the program.

In the past, only a few languages such as Smalltalk provided purely object-oriented solutions. These solutions executed far slower than conventional procedural languages such as C. C was also more efficient than such languages. However, C++ provides the extension required for object orientation to C, and at the same time provides almost the same efficiency as C. Therefore, the object-oriented model is not imposed on the developer such as in Java.

C++ is designed to give freedom to programmers and hence it does not impose the object-oriented model, unlike Java.

We can choose between object-based programming (which is less flexible but more efficient) and object-oriented programming (which is more flexible but less efficient). C++ provides a balance between the efficiency of C and the flexibility of an object-oriented or object-based design. This is why, even after more than a decade of its inception, C++ is still very popular among the developer community.

C++ provides a choice to the programmer to decide whether he/she needs an object-based or an object-oriented design.

## Differences between Object-based and Object-oriented Programming

In this section, we briefly outline the differences between object-based and object-oriented programming.

Object-based programming Object-based programming uses objects and classes but without inheritance. It provides flexibility to the program and is easier to work with. Operator overloading, function overloading, and the use of constructors and destructors are included in object-based programming.

![](img/0da15892b2796544fb447dc5727e9ab4_31_0.png)

## Fig. 1.3 Inter-relationship between programs and entities

marksheet printing, the third is maintaining the subject (i.e., provide adding, deleting, and modifying details of a subject), and the fourth is maintaining the teacher's information (i.e., providing adding, deleting, and modifying details of a teacher). There are five entities considered—roll call, teacher, student, marksheet, and subject. Again, there are possibly many more, but they have not been considered for simplicity. Figure 1.3 shows the association of each entity with each program. The actual system design process might generate a large number of programs and a larger number of entities in more than one way. The following example will illustrate the concept.

![](img/0da15892b2796544fb447dc5727e9ab4_31_1.png)

## Fig. 1.4 Determining relations among entities

Once we decide the data and function attributes of the program, the next step is to find the relation between the different entities by asking a few simple questions.

‘How is a teacher associated with the roll call?’ is one such question. One answer may associate a teacher with the roll call as the person who takes it for his/her subject. We may need to obtain the information about the corresponding teacher from the roll call entity. Figure 1.4 shows an example of a message being asked and replies being sought from an entity. The question or the query is normally referred to as a request and the reply is termed as the response.

> When a program uses objects to represent real-world entities, its end users ask queries to the objects and seek responses by passing and receiving messages.

When we look at our job to be done, we need to have few more such cases of requests and responses, for example, a teacher asking how many students were present on a particular day in the class and the roll call entity answering that question. We may need to find out how many such questions are possible to be asked and how the answers to these questions are sought out. This is the next assignment when we are developing our system. The method to generate the answer of a message must be provided to the receiving entity; otherwise, the receiving entity cannot answer that question. In the case of the question regarding the number of students present, the roll call entity must have a method to calculate the total students present from the data it has. This method is called or invoked by the receiving entity when the other entity asks for that specific information.

## 1.3 CLASSES AND OBJECTS

A class is an extension to the C struct (the basic C struct is also extended in C++; we will examine the difference later). Let us consider an example of a class Student. The struct Student in C will contain only the attributes of the student such as name and address. On the other hand, in C++, the class Student will have the attributes of the student and it will also store the actions (or functions) related to the student. This means that the student class will contain the student name, address, roll number, subjects, etc., as well as all actions in

the form of functions to be performed on the variables of that class or by the variables of that class (the variables of the class Student are student1, student2, etc., which are actual students and are known as student objects).

The words on and by used in the previous statement have an important meaning. It is possible to have any function inside any class, but it is not recommended. Only functions that describe the actions of the entity under consideration should be a part of the entity and others should not be included. We will elaborate this issue further with appropriate examples in Chapter 4.

Note There is no restriction on the type of function a class can have, but a good design requires only related functions to be a part of the class.

There is one design methodology that demands that classes be designed with minimal member functions. It says that when we design classes, we should not keep a function as a member function unless it is necessary. This will make a class ‘thin’ and easy to modify or extend.

Note The thin class design requires only necessary functions and data attributes to be part of a class, in a way making it easy to administer. When a class has less number of member functions, it is less affected when the class grows or changes.

Thus, the functions for reading and printing information about a student, enrolling of the student in a class, and other functions, which we may consider useful for solving our problem, will also be a part of the Student class. Here, we must understand the difference between the student class and the student object. A class is a data type and an object is a variable of that data type. A Student class is an abstraction describing what a student object should have (name, address, etc.) and should do (printing details, accepting details, checking whether passed or not, etc.), but does not do anything itself. A student object is an instance of that class, which actually has a name, an address, etc. A class is a sketch from where actual objects are derived. If we have a Student class to represent 30 students, we have one student class and 30 objects of it. The action performed by the objects (i.e., the variables of type class) is known as method in object-oriented programming, but C++ calls it function. So we will use the word ‘function’ to describe the action that is performed on or by an object of the class.

Operations are performed by and on objects and not classes.

The functions that are a part of the class are known as member functions. A member function helps programmers to control its access.

The objects of the class alone can operate on the functions owned by them.

The functions that are a part of the class are known as member functions. It is also possible to have functions that do not belong to any class; such functions are known as non-member functions. In C struct, functions are not a part of the struct; if they need to operate on a structure, it is passed to them. For example, StudentPrintDetails() function is a separate function from struct Student. It cannot become a part of struct Student. A struct variable representing student must be passed to that function for printing the information about the student. If we have defined struct Student Lara, then calling StudentPrintDetails(Lara) requires Lara to be passed to the function. The StudentPrintDetails() function is neither a part of struct Student nor has any compulsion not to be seen by variables other than of type struct. If we define struct Student Mahesh, then we may use StudentPrintDetails(Mahesh) to print details about Mahesh. However, we can also pass something else to the function. If Snoopy is a variable of type struct dog, we can write StudentPrintDetails((Student) Snoopy). This process may print garbage on the screen, but the compiler will not be able to judge
