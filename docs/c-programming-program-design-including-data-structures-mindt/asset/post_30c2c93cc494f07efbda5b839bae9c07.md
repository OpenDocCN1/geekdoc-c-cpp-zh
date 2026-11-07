
In C++, a function name and operators such as `+`, `-`, `*`, and `/` can be overloaded. An example of function overloading occurs when the function or operator is called, and the specific version used is decided according to the arguments used. For instance, if both operands are integers, the division operator yields an integer result; otherwise, the division operator yields a decimal result. Suppose a class has constructors. If no arguments are passed to an object when it is declared, the default constructor is executed; otherwise, one of the constructors with parameters is executed. However, all constructors have the same name.

C++ also provides parametric polymorphism. In parametric polymorphism, the (data) type is left unspecified and then later instantiated. Templates (discussed in Chapter 13) provide parametric polymorphism. Also, C++ provides virtual functions as a means to implement polymorphism in an inheritance hierarchy, which allows the run-time selection of appropriate member functions. (Chapter 12 discusses virtual functions.)

There are several OOP languages in existence today, including Ada, Modula-2, Eiffel, C++, Java, Python, C#, and Smalltalk. The earliest OOP language was Simula, developed in 1967. The OOP terminology is influenced by the vocabulary of Smalltalk, the OOP language largely developed at a Xerox research center during the 1970s. An OOP language uses many “fancy” words, such as methods, message passing, and so forth.

OOP is a natural and intuitive way to view the programming process. When we view an object, we immediately think of what it can do. For example, when we think about a car, we also think about the operations on the car, such as starting the car and driving the car. When programmers think about a list, they also think about the operations on the list, such as searching, sorting, and inserting. OOP allows ADT to be created and used. In C++, we implement ADT through the use of classes. Objects are created when class variables are declared. Objects interact with each other via function calls. Every object has an internal state and an external state. The `private` members form the internal state; the `public` members form the external state. Only the object can manipulate its internal state.

## Identifying Classes, Objects, and Operations

In this book’s first nine chapters, in the problem analysis phase, we analyzed the problem, identified the data, and outlined the algorithm. To reduce the complexity of the function main, we wrote functions to manipulate the data. In Chapter 10, we used the OOD technique and first identified the objects that made up the overall problem. The objects were designed and implemented independently of the main program. The hardest part in OOD is to identify the classes and objects. In this section, we describe a common and simple technique to identify classes and objects.

We begin with a description of the problem and then identify all of the nouns and verbs. We choose our classes from the list of nouns, and we choose our operations from the list of verbs.

For example, suppose that we want to write a program that calculates and prints the volume and surface area of a cylinder. We can state this problem as follows:

*Write a* **program** *to input the* **dimensions** *of a* **cylinder** *and calculate and print the* **surface area** *and* **volume**.

In this statement, the nouns are bold, and the verbs are italic. From the list of nouns—**program**, **dimensions**, **cylinder**, **surface area**, and **volume**—we can easily visualize **cylinder** to be a class—say, *cylinderType*—from which we can create many cylinder objects of various dimensions. The nouns **dimensions**, **surface area**, and **volume** are characteristics of a **cylinder** and thus can hardly be considered classes.

After we identify a class, the next step is to determine three pieces of information:

- Operations that an object of that class type can perform
- Operations that can be performed on an object of that class type
- Information that an object of that class type must maintain

From the list of verbs identified in the problem description, we choose a list of possible operations that an object of that class can perform, or has performed, on itself. For example, from the list of verbs for the cylinder problem description—*write, input, calculate,* and *print*—the possible operations for a cylinder object are *input, calculate,* and *print*.

For the class **cylinderType**, the dimensions represent the data. The center of the base, radius of the base, and height of the cylinder are the characteristics of the dimensions. You input data to the object either by a constructor or by a mutator function.

The verb *calculate* applies to determining the volume and the surface area. From this, you can deduce the operations: **cylinderVolume** and **cylinderSurfaceArea**. Similarly, the verb *print* applies to the display of the volume and the surface area on an output device. In Programming Exercise 3 at the end of this chapter, you are asked to design a class to implement the characteristics of a cylinder.

Identifying classes via the nouns and verbs from the descriptions of the problem is not the only technique possible. There are several other OOD techniques in the literature. However, this technique is sufficient for the programming exercises in this book.

## PROGRAMMING EXAMPLE: Grade Report

![](img/b217c421655b51e7494cf3b89bb5432d_830_0.png)

This programming example further illustrates the concepts of inheritance and composition.

The mid-semester point at your local university is approaching. The registrar’s office wants to prepare the grade reports as soon as the students’ grades are recorded. However, some of the students enrolled have not yet paid their tuition.

1. If a student has paid the tuition, the grades are shown on the grade report together with the grade point average (GPA).
2. If a student has not paid the tuition, the grades are not printed. For these students, the grade report contains a message indicating that the grades have been held for nonpayment of the tuition. The grade report also shows the billing amount.

The registrar's office and the business office want your help in writing a program that can analyze the students' data and print the appropriate grade reports. The data is stored in a file in the following form:

```
studentCount tuitionRate
studentName studentID isTuitionPaid numberOfCourses
courseName courseNumber creditHours grade
courseName courseNumber creditHours grade
.
.
.
studentName studentID isTuitionPaid numberOfCourses
courseName courseNumber creditHours grade
courseName courseNumber creditHours grade
.
.
.
```

The first line indicates the number of students enrolled and the tuition rate per credit hour. The students' data is given thereafter. A sample input file is as follows:

```
3 345
Lisa Miller 890238 Y 4
Mathematics MTH345 4 A
Physics PHY357 3 B
ComputerSci CSC478 3 B
History HIS356 3 A
.
.
.
```

The first line indicates that the input file contains three students' data, and the tuition rate is $345 per credit hour. Next, the course data for student Lisa Miller is given: Lisa Miller's ID is 890238, she has paid the tuition, and she is taking four courses. The course number for the mathematics class she is taking is MTH345, the course has four credit hours, her mid-semester grade is A, and so on. The desired output for each student is in the following form:

```
Student Name: Lisa Miller
Student ID: 890238
Number of courses enrolled: 4
```

| Course No | Course Name | Credits | Grade |
|---|---|---|---|
| CSC478 | ComputerSci | 3 | B |
| HIS356 | History | 3 | A |
| MTH345 | Mathematics | 4 | A |
| PHY357 | Physics | 3 | B |

Total number of credits: 13  
Mid-Semester GPA: 3.54

It is clear from this output that the courses must be ordered according to the course number. To calculate the GPA, we assume that the grade A is equivalent to four points, B is equivalent to three points, C is equivalent to two points, D is equivalent to one point, and F is equivalent to zero points.

Input: A file containing the data in the form given previously. For easy reference, let us assume that the name of the input file is stData.txt.

Output: A file containing the output in the form given previously.

## PROBLEM ANALYSIS AND ALGORITHM DESIGN

### Course

We must first identify the main components of the program. The university has students, and every student takes courses. Thus, the two main components are the student and the course.

Let us first describe the course component.

The main characteristics of a course are the course name, course number, and number of credit hours.

Some of the basic operations that need to be performed on an object of the course type are as follows:

1. Set the course information.
2. Print the course information.
3. Show the credit hours.
4. Show the course number.

The following class defines the course as an ADT:

```cpp
class courseType
{
public:
    void setCourseInfo(string cName, string cNo, int credits);
    //Function to set the course information.
    //The course information is set according to the
    //parameters.
    //Postcondition: courseName = cName; courseNo = cNo;
    //               courseCredits = credits;
```
