resents the last employee type. The UML class diagram in Fig. 13.7 shows the inheritance hierarchy for our polymorphic employee payroll application. The abstract class name *Employee* is italicized, as per the convention of the UML.

![](bbox=[0.143, 0.175, 0.857, 0.377])

**Fig. 13.7**  |  *Employee hierarchy UML class diagram.*

Abstract base class Employee declares the “interface” to the hierarchy—that is, the set of member functions that a program can invoke on all Employee objects. Each employee, regardless of the way his or her earnings are calculated, has a first name, a last name and a social security number, so private data members firstName, lastName and socialSecurityNumber appear in abstract base class Employee.

> **Software Engineering Observation 13.1.1**
> 
> *A derived class can inherit interface and/or implementation from a base class. Hierarchies designed for implementation inheritance tend to have their functionality high in the hierarchy—each new derived class inherits one or more member functions that were defined in a base class, and the derived class uses the base-class definitions. Hierarchies designed for interface inheritance tend to have their functionality lower in the hierarchy—a base class specifies one or more functions that should be defined for each class in the hierarchy (i.e., they have the same prototype), but the individual derived classes provide their own implementations of the function(s).*

The following sections implement the Employee class hierarchy. The first five each implement one of the abstract or concrete classes. The last section implements a test program that builds objects of all these classes and processes the objects polymorphically.

# 13.6.1 Creating Abstract Base Class Employee

Class Employee (Figs. 13.9–13.10, discussed in further detail shortly) provides functions earnings and print, in addition to various get and set functions that manipulate Employee’s data members. An earnings function certainly applies generally to all employees, but each earnings calculation depends on the employee’s class. So we declare earnings as pure virtual in base class Employee because a default implementation does not make sense for that function—there is not enough information to determine what amount earnings should return. Each derived class overrides earnings with an appropriate implementation. To calculate an employee’s earnings, the program assigns the address of an employee’s ob-