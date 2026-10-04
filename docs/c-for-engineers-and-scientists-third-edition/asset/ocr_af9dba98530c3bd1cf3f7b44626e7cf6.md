# Chapter 10 581

A Case Study: Constructing a Room
Object

Your program should display the area of each room and the total area of all rooms
combined.

+   b. The total area of all rooms can be calculated and saved by a class variable. To
do this, what type of value do you think this class must be?

+   4. (Debug) Remove the public access from the RoomType function declarations in
Program 10.4 and compile the program. Determine whether the compiler returns error
messages that it does.

+   5. (Program) a. Complete the following class by adding a constructor, an accessor, and a
function calculation. The constructor should initialize all objects with firstNumber = 10
and secondNumber = 15. The function should calculate and display the average-
of the two numbers.

```
class TwoNumbers
{
    // class declaration section
    private
    int firstNumber;
    int secondNumber;
    double average;
}

// class implementation section
```

+   b. Include the class for Exercise 5a in the context of a complete program. The
program should create a single object and display the object's values and the average
of these values.

+   6. (Program) a. Construct a Time class containing the integer instance variables
minutes, and hours. Include a constructor that initializes each data with a member
value of 10 and an accessor that displays the value of all data members.

+   b. Include the class for Exercise 6a in the context of a complete program.

+   7. (Program) Construct a class Light that simulates a traffic light. The class's
attribute should change from Green to Yellow to Red and then back to Green
using the class's change() function. When a new Light object is created, its initial
color should be Red.

+   8. (Program) a. Construct a class Student containing an integer student ID
and a double-precision grade point average. The constructor for this class should
initialize the ID to 111111 and the grade point to 0.0. Include an access-
or to display all data.

+   b. Include the class constructed in Exercise 8a in the context of a complete program.
Your program should declare two objects of type Student and display for the
two objects to verify the operation of the class functions.

+   9. (Program) a. Construct a class definition to represent an employee of a company. Each
employee is defined by an integer ID, a floating-point pay rate, and the maxi-
number of hours the employee should work each week. The services the class prov-
 the capability to enter data for a new employee, the capability to change
data for a new employee, and the capability to display existing data for a new employee.