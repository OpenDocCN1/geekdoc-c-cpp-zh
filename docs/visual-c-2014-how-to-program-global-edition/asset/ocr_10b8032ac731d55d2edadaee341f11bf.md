# 11.2 Base Classes and Derived Classes 477

trust, has-a represents composition (see Chapter 10). In a has-a relationship, an object contains members references to other objects. For example, a car has a steering wheel, and a car object has a reference to a steering-wheel object.

New classes can inherit from class libraries. Organizations develop their own class libraries and take advantage of others available worldwide. Some, most new software will be constructed from standardized components, just as automobiles and most computer hardware are constructed today. This will facilitate the development of more powerful, abundant and economical software.

# 11.2 Base Classes and Derived Classes

Often, an object of one class is an object of another class. For example, in geometry, a rectangle is a quadrilateral (as squares, parallelograms and trapezoids). Thus, class Rectangle can be inherited from class Quadrilateral. In this context, Quadrilateral is a base class and class Rectangle is a derived class. A rectangle is a specific type of quadrilateral, but it's incorrect to claim that quadrilateral is a rectangle—the quadrilateral could be a parallelogram or some other shape. Figure 11.1 lists several examples of base classes and derived classes—base classes tend to be more general, and derived classes tend to be more specific.

| Base class | Derived classes |
| --- | --- |
| Student | GraduateStudent, UndergraduateStudent |
| Shape | Circle, Triangle, Rectangle |
| Loan | CarLoan, HomeImprovementLoan, MortgageLoan |
| Employee | Faculty, Staff, HourlyWorker, CommissionWorker |
| SpaceObject | Star, Moon, Planet, FlyingSaucer |
| BankAccount | CheckingAccount, SavingsAccount

> **Fig. 11.1** | Inheritance examples.

Because every derived-class is an object of its base class, and one base class can have many derived classes, the set of objects represented by a base class is typically larger than the set of objects represented by any of its derived classes. For example, the base class Vehicle represents all vehicles—cars, trucks, bicycles and so on. By contrast, derived car represents a smaller, more specific subset of vehicles.

Inheritance relationships form hierarchical structures (Figs. 11.2 and 11.3). A base class exists in a hierarchical relationship with its derived classes. When classes participate in inheritance, they become "affiliated" with other classes. A class becomes either a base class, supplying members to other, or a derived class, inheriting its members from another class. Sometimes, a class is both a base and a derived class.

Let us develop a sample class hierarchy, also called an inheritance hierarchy (Fig. 11.2). The UML class diagram of 11.2 shows a university community that has many types of members, including employees, students and alumni. Employees are either faculty members or staff members. Faculty members are either administrators (such as deans and department chairs) or teachers. The hierarchy could contain many other