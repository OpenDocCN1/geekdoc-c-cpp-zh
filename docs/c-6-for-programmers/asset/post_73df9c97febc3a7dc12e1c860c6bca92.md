
and to the devices. For each device, the operating system uses a piece of software called a device driver to control all communication between the system and the device. The write message sent to a device-driver object needs to be interpreted specifically in the context of that driver and how it manipulates a specific device. However, the write call itself really is no different from the write to any other device in the system: Place some number of bytes from memory onto that device. An object-oriented operating system might use an abstract base class to provide an "interface" appropriate for all device drivers. Then, through inheritance from that abstract base class, derived classes are formed that all behave similarly. The device-driver methods are declared as abstract methods in the abstract base class. The implementations of these abstract methods are provided in the derived classes that correspond to the specific types of device drivers. New devices are always being developed, often long after the operating system has been released. When you buy a new device, it comes with a device driver provided by the device vendor. The device is immediately operational after you connect it to your computer and install the device driver. This is another elegant example of how polymorphism makes systems extensible.

## 12.5 Case Study: Payroll System Using Polymorphism

This section reexamines the CommissionEmployee-BasePlusCommissionEmployee hierarchy that we explored in Section 11.4. Now we use an abstract method and polymorphism to perform payroll calculations based on the type of employee. We create an enhanced employee hierarchy to solve the following problem:

> A company pays its employees on a weekly basis. The employees are of four types:

- 1. Salaried employees are paid a fixed weekly salary regardless of the number of hours worked.
- 2. Hourly employees are paid by the hour and receive "time-and-a-half" overtime pay for all hours worked in excess of 40 hours.
- 3. Commission employees are paid a percentage of their sales.
- 4. Salaried-commission employees receive a base salary plus a percentage of their sales.

> For the current pay period, the company has decided to reward salaried-commission employees by adding 10% to their base salaries. The company wants to implement an app that performs its payroll calculations polymorphically.

We use abstract class Employee to represent the general concept of an employee. The classes that extend Employee are SalariedEmployee, CommissionEmployee and HourlyEmployee. Class BasePlusCommissionEmployee—which extends CommissionEmployee—represents the last employee type. The UML class diagram in Fig. 12.2 shows the inheritance hierarchy for our polymorphic employee payroll app. Abstract class Employee is italicized, as per the convention of the UML.

Abstract base class Employee declares the "interface" to the hierarchy—that is, the set of members that an app can invoke on all Employee objects. We use the term "interface" here in a general sense to refer to the various ways apps can communicate with objects of any Employee derived class. Be careful not to confuse the general notion of an "interface" with the formal notion of a C# interface, the subject of Section 12.7. Each employee, regardless of the way his or her earnings are calculated, has a first name, a last name and a social security number, so those pieces of data appear in abstract base class Employee.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_372_0.png)

Fig. 12.2 | Employee hierarchy UML class diagram.

The following subsections implement the Employee class hierarchy. Section 12.5.1 implements abstract base class Employee. Sections 12.5.2–12.5.5 each implement one of the concrete classes. Section 12.5.6 implements a test app that builds objects of all these classes and processes those objects polymorphically.

### 12.5.1 Creating Abstract Base Class Employee

Class Employee (Fig. 12.4) provides methods Earnings and ToString, in addition to the auto-implemented properties that manipulate Employee’s data. An Earnings method certainly applies generically to all employees. But each earnings calculation depends on the employee’s class. So we declare Earnings as abstract in base class Employee, because a default implementation does not make sense for that method—there’s not enough information to determine what amount Earnings should return. Each derived class overrides Earnings with a specific implementation. To calculate an employee’s earnings, the app assigns a reference to the employee’s object to a base class Employee variable, then invokes the Earnings method on that variable. We maintain a List of Employee variables, each of which holds a reference to an Employee object (of course, there cannot be Employee objects because Employee is an abstract class—because of inheritance, however, all objects of all derived classes of Employee may nevertheless be thought of as Employee objects). The app iterates through the List and calls method Earnings for each Employee object. These method calls are processed polymorphically. Including Earnings as an abstract method in Employee forces every directly derived concrete class of Employee to override Earnings with a method that performs an appropriate pay calculation.

Method ToString in class Employee returns a string containing the employee’s first name, last name and social security number. Each derived class of Employee overrides method ToString to create a string representation of an object of that class containing the employee’s type (e.g., “salaried employee:”), followed by the rest of the employee’s information.

The diagram in Fig. 12.3 shows each of the five classes in the hierarchy down the left side and methods Earnings and ToString across the top. For each class, the diagram shows the desired results of each method. [Note: We do not list base class Employee’s properties because they’re not overridden in any of the derived classes—each of these properties is inherited and used “as is” by each of the derived classes.]

| Class | Earnings | ToString |
|---|---|---|
| Employee | abstract | firstName lastName social security number: SSN |
| Salaried-Employee | weeklySalary | salaried employee: firstName lastName social security number: SSN weekly salary: weeklySalary |
| Hourly-Employee | if hours <= 40 wage * hours if hours > 40 40 * wage + (hours - 40) * wage * 1.5 | hourly employee: firstName lastName social security number: SSN hourly wage: wage hours worked: hours |
| Commission-Employee | commissionRate * grossSales | commission employee: firstName lastName social security number: SSN gross sales: grossSales commission rate: commissionRate |
| BasePlus-Commission-Employee | baseSalary + (commissionRate * grossSales) | base salaried commission employee: firstName lastName social security number: SSN gross sales: grossSales commission rate: commissionRate base salary: baseSalary |

Fig. 12.3 | Polymorphic interface for the Employee hierarchy classes.

### Class Employee

Let's consider class Employee's declaration (Fig. 12.4). The class includes auto-implemented, getter-only properties for the first name, last name and social security number (lines 5-7); a constructor that initializes the first name, last name and social security number (lines 10-16); expression-bodied method ToString (lines 19-20), which uses properties to return an Employee's string representation; and abstract method Earnings (line 23), which must be implemented by concrete derived classes. The Employee constructor does not validate the social security number in this example. Normally, such validation should be provided.

```csharp
1 // Fig. 12.4: Employee.cs
2 // Employee abstract base class.
3 public abstract class Employee
4 {
5     public string FirstName { get; }
6     public string LastName { get; }
7     public string SocialSecurityNumber { get; }
```

Fig. 12.4 | Employee abstract base class. (Part 1 of 2.)
