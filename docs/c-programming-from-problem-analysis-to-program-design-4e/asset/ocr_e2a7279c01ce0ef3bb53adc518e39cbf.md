It should not be possible to create a group in this application unless it is associated with a club, fraternity, sorority, or intramural team.

# DESIGN A SOLUTION

The desired output is to display data on a Windows form about the different organizations. An application is created using the Windows Form class to test the design. It should ensure that objects can be instantiated from the Club, FratSorority, and Intramural classes, but not from the Organization class. It should make sure that derived classes have access to base class members. Figure 11-19 shows a prototype for the form.

![](bbox=[0.201, 0.321, 0.7, 0.638])

**FIGURE 11-19** Prototype for StudentGov example

The business logic is separated into several classes to include an Organization class that serves as a base class. No objects should be instantiated from this class, so it is defined as an abstract class. Derived classes of Club, Intramural, and FratSorority are defined to inherit from the Organization class. The IFunding interface is defined to force functionality of setting the funding amount. FratSorority and Club both implement this interface.

Class diagrams are used to help design and document these characteristics. Figure 11-20 shows the class diagrams for the StudentGov example.