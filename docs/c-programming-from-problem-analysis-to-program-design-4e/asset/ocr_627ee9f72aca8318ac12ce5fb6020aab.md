# PROGRAMMING EXAMPLE: TempAgency Application

This example demonstrates the design and implementation of a graphical user interface for a Windows application. Two classes are constructed to separate the business logic from the presentation details. The first class defines a template for a typical payroll employee object. It includes the behaviors for determining withholding deductions and calculating the net take-home pay; thus, the business logic is described in this Employee class. The other class instantiates an object of the Employee class and instantiates a Windows Form object to represent the graphical user interface. Using the .NET predefined Control classes, labels, text boxes, and button objects are added to the Form object. The problem specification for the TempAgency application is shown in Figure 9-16.

![](bbox=[0.1856, 0.3486, 0.6951, 0.8333])

FIGURE 9-16  Problem specification for TempAgency

# ANALYZE THE PROBLEM

You should review the problem specification in Figure 9-16 and make sure you understand the problem definition. Several values will be entered into the program to represent the name, number of hours worked, and number of dependents for an employee. The business logic is separated from the user interface by using two separate