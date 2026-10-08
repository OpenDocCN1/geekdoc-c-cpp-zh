# Chapter 12 OOP: Polymorphism and Interfaces

![](bbox=[0.147, 0.115, 0.852, 0.292])

**Fig. 12.2** Employee hierarchy UML class diagram.

The following subsections implement the Employee class hierarchy. Section 12.5.1 implements abstract base class Employee. Sections 12.5.2–12.5.5 each implement one of the concrete classes. Section 12.5.6 implements a test app that builds objects of all these classes and processes those objects polymorphically.

# 12.5.1 Creating Abstract Base Class Employee

Class Employee (Fig. 12.4) provides Earnings and ToString, in addition to the auto-implemented properties that manipulate Employee’s data. Each method generally applies to all employees. But each Earnings calculation depends on the employee’s class. We declare Earnings as abstract in base class Employee, because a default implementation does not make sense for that method—there’s not enough information to determine what amount Earnings should return. Derived classes override Earnings with a specific implementation. The app assigns a reference to the employee’s object to a base Employee variable, then invokes the Earnings method on that variable. We maintain a List of Employee variables, each of which holds a reference to an Employee object (of course, cannot be Employee objects because Employee is an abstract class—because of inheritance, all of these derived classes are objects). The app iterates through the List and calls method for each Employee object. These methods are called polymorphically. Including Earnings as an abstract method in Employee forces every directly derived class of Employee to override Earnings with a method that performs an appropriate calculation.

ToString in class Employee returns a string containing the employee’s first name, last name and social security number. Each derived class of Employee overrides ToString to create a string representation of an object of that class containing the employee’s type (e.g., “salaried employee:\), followed by the rest of the employee’s information.

The diagram in Fig. 12.3 shows each of the five classes in the hierarchy down the left side and methods of Earnings and ToString across the top. For each class, the diagram shows the result of each method. [Note: We do not list base Employee’s properties because they are not overridden in any of the derived classes—each of these properties is inherited and used “as is” by each of the derived classes.]