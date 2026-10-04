# Introduction to Classes

+   10. (Practice) a. Construct a class diagram for a computer that consists of a monitor, keyboard, mouse, printer, and system box.

+   b. Modify the class diagram constructed in Exercise 10a to denote that one or more monitors and keyboards might be attached to the system box, and the system might have no mouse or multiple mice.

+   c. Extend the class diagram constructed for Exercise 10b to denote that the system box is composed of a CPU chip, a memory board containing zero or more RAM chips, and case.

+   11. (Practice) a. Construct a class diagram for a single gas tank connected to one or more gas pumps. The attributes of interest for the tank are its capacity, current level, and grade of gas. The attributes of interest for pump are the number of gallons dispensed and the cost per gallon. A pump responds to being enabled and disabled.

+   b. Modify the class diagram constructed in Exercise 11a to denote that a gas pump can be associated with more than one gas tank.

+   12. (Practice) Construct a class diagram for class of circles that are the base class for a class of spheres and a class of cylinders.

+   13. (Practice) Construct a class diagram for a collection of cards consisting of zero or more cards. The collection of cards forms a base class for both a deck of cards and a hand of cards.

+   14. (Practice) Determine a car's major subsystems, such as brakes, steering, and so forth. Considering these subsystems as classes, construct a class diagram for a Car class that simply shows the associations between classes (no attributes or operations). Then determine a set of attributes and operations for each subsystem, and modify the original class diagram to include the additional information.

+   15. (Practice) Determine a cell phone's major subsystems, such as keypad, antenna, and so on. Considering these subsystems as classes, construct a class diagram for a CellPhone class that simply shows the associations between classes (no attributes or operations). Then determine a set of attributes and operations for each subsystem, and modify the original class diagram to include the additional information.

# 10.5 Common Programming Errors

Some programming errors associated with constructing classes are as follows:

+   1. Failing to terminate the class declaration section with a semicolon.

+   2. Including a return type with the constructor's prototype or failing to include a return type with the other functions' prototypes.

+   3. Using the same name for a data member as a member function.

+   4. Defining more than one default constructor for a class.

+   5. Forgetting to include the class name and scope operator, ::, in the function header of all member functions defined in the class implementation section.

All these errors result in a compiler error message.