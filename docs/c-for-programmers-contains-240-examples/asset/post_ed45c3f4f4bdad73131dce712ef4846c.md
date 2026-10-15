
faster. In a sense, the pedal “hides” the complex mechanisms that actually make the car go faster, just as the brake pedal “hides” the mechanisms that slow the car, the steering wheel “hides” the mechanisms that turn the car and so on. This enables people with little or no knowledge of how cars are engineered to drive a car easily, simply by using the accelerator pedal, the brake pedal, the steering wheel, the transmission shifting mechanism and other such simple and user-friendly “interfaces” to the car’s complex internal mechanisms.

Unfortunately, you cannot drive the engineering drawings of a car—before you can drive a car, it must be built from the engineering drawings that describe it. A completed car will have an actual accelerator pedal to make the car go faster. But even that’s not enough—the car will not accelerate on its own, so the driver must press the accelerator pedal to tell the car to go faster.

## Classes and Member Functions

Now let’s use our car example to introduce the key object-oriented programming concepts of this section. Performing a task in a program requires a function (such as main, as described in Chapter 2). The function describes the mechanisms that actually perform its tasks. The function hides from its user the complex tasks that it performs, just as the accelerator pedal of a car hides from the driver the complex mechanisms of making the car go faster. In C++, we begin by creating a program unit called a class to house a function, just as a car’s engineering drawings house the design of an accelerator pedal. Recall from Section 1.10 that a function belonging to a class is called a member function. In a class, you provide one or more member functions that are designed to perform the class’s tasks. For example, a class that represents a bank account might contain one member function to deposit money into the account, another to withdraw money from the account and a third to inquire what the current account balance is.

## Objects

Just as you cannot drive an engineering drawing of a car, you cannot “drive” a class. Just as someone has to build a car from its engineering drawings before you can actually drive the car, you must create an object of a class before you can get a program to perform the tasks the class describes. That is one reason C++ is known as an object-oriented programming language. Note also that just as many cars can be built from the same engineering drawing, many objects can be built from the same class.

## Requesting an Object’s Services via Member-Function Calls

When you drive a car, pressing its gas pedal sends a message to the car to perform a task—that is, make the car go faster. Similarly, you send messages to an object—each message is known as a member-function call and tells a member function of the object to perform its task. This is often called requesting a service from an object.

## Attributes and Data Members

Thus far, we have used the car analogy to introduce classes, objects and member functions. In addition to the capabilities a car provides, it also has many attributes, such as its color, the number of doors, the amount of gas in its tank, its current speed and its total miles driven (i.e., its odometer reading). Like the car’s capabilities, these attributes are represented as part of a car’s design in its engineering diagrams. As you drive a car, these attributes are always associated with the car. Every car maintains its own attributes. For example, each car knows how much gas is in its own gas tank, but not how much is in the tanks of other cars. Similarly, an object has attributes that are carried with the object as it is used in a program. These attributes are specified as part of the object’s class. For example, a bank account object has a balance attribute that represents the amount of money in the account. Each bank account object knows the balance in the account it represents, but not the balances of the other accounts in the bank. Attributes are specified by the class’s data members.

## 3.3 Overview of the Chapter Examples

The remainder of this chapter presents seven simple examples that demonstrate the concepts we introduced in the context of the car analogy. These examples, summarized below, incrementally build a GradeBook class to demonstrate these concepts:

- 1. The first example presents a GradeBook class with one member function that simply displays a welcome message when it is called. We show how to create an object of that class and call the member function so that it displays the welcome message.
- 2. The second example modifies the first by allowing the member function to receive a course name as a so-called argument. Then, the member function displays the course name as part of the welcome message.
- 3. The third example shows how to store the course name in a GradeBook object. For this version of the class, we also show how to use member functions to set the course name in the object and get the course name from the object.
- 4. The fourth example demonstrates how the data in a GradeBook object can be initialized when the object is created—the initialization is performed by a special member function called the class’s constructor. This example also demonstrates that each GradeBook object maintains its own course name data member.
- 5. The fifth example modifies the fourth by demonstrating how to place class GradeBook into a separate file to enable software reusability.
- 6. The sixth example modifies the fifth by demonstrating the good software-engineering principle of separating the interface of the class from its implementation. This makes the class easier to modify without affecting any clients of the class’s objects—that is, any classes or functions that call the member functions of the class’s objects from outside the objects.
- 7. The last example enhances class GradeBook by introducing data validation, which ensures that data in an object adheres to a particular format or is in a proper value range. For example, a Date object would require a month value in the range 1–12. In this GradeBook example, the member function that sets the course name for a GradeBook object ensures that the course name is 25 characters or fewer. If not, the member function uses only the first 25 characters of the course name and displays a warning message.

Note that the GradeBook examples in this chapter do not actually process or store grades. We begin processing grades with class GradeBook in Chapter 4 and we store grades in a GradeBook object in Chapter 7, Arrays and Vectors.

## 3.4 Defining a Class with a Member Function

We begin with an example (Fig. 3.1) that consists of class GradeBook (lines 9–17), which represents a grade book that an instructor can use to maintain student test scores, and a main function (lines 20–25) that creates a GradeBook object. Function main uses this object and its member function to display a message on the screen welcoming the instructor to the grade-book program.

First we describe how to define a class and a member function. Then we explain how an object is created and how to call a member function of an object. The first few examples contain function main and the GradeBook class it uses in the same file. Later in the chapter, we introduce more sophisticated ways to structure your programs to achieve better software engineering.

```
1  // Fig. 3.1: fig03_01.cpp
2  // Define class GradeBook with a member function displayMessage,
3  // create a GradeBook object, and call its displayMessage function.
4  #include <iostream>
5  using std::cout;
6  using std::endl;
7
8  // GradeBook class definition
9  class GradeBook
10 {
11 public:
12     // function that displays a welcome message to the GradeBook user
13     void displayMessage()
14     {
15         cout << "Welcome to the Grade Book!" << endl;
16     } // end function displayMessage
17 }; // end class GradeBook
18
19 // function main begins program execution
20 int main()
21 {
22     GradeBook myGradeBook; // create a GradeBook object named myGradeBook
23     myGradeBook.displayMessage(); // call object's displayMessage function
24     return 0; // indicate successful termination
25 } // end main
```

Welcome to the Grade Book!

Fig. 3.1 | Define class GradeBook with a member function displayMessage, create a GradeBook object, and call its displayMessage function.

## Class GradeBook

Before function main (lines 20–25) can create an object of class GradeBook, we must tell the compiler what member functions and data members belong to the class. The GradeBook class definition (lines 9–17) contains a member function called displayMessage (lines 13–16) that displays a message on the screen (line 15). Recall that a class is like a blueprint—so we need to make an object of class GradeBook (line 22) and call its dis-
