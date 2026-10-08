# Chapter 12 OOP: Polymorphism and Interfaces

To implement more than one interface, use a comma-separated list of interface names
after the colon (:) in the class declaration, as in

```
public class ClassName : BaseClassName, FirstInterface, SecondInterface, ...
```

When a class inherits from a base class and implements one or more interfaces, the class
declaration must list the base-class name before any interfaces.

> Software Engineering Observation 12.6
C does not allow derived classes to inherit from more than one class, but it does allow
a class to inherit from a base class and implement any number of interfaces.

Class Invoice implements the one method in interface IPayment—method GetGetPaymentAmount is declared in line 66. The method calculates the amount required to pay
the method multiplies the values of quantity and pricePerItem (obtained
through the appropriate properties) and returns the result. This method satisfies the
implementation requirement for the method in interface IPayment—we fulfilled the
interface contract with the compiler.

# 12.7 Modifying Class Employee to Implement Interface IPayment

We now modify Employee to implement interface IPayment (Fig. 12.13). This class
declaration is identical to that of Fig.12.4 with two exceptions:

+   - Line 3 of Fig.12.13 indicates that class Employee now implements interface IPayment.
- Line 27 implements interface IPayment's GetPaymentAmount method.

Notice that GetPaymentAmount calls Employee's abstract method Earnings. At
execution, when it is called on an object of an derived
class, GetPaymentAmount calls that's concrete Earnings method, which knows how
to calculate earnings for objects of derived-type class.

```
// Fig. 12.13 | Employee.cs
// Employee abstract base class that implements interface IPayment
public abstract class Employee : IPayment
{
    public string FirstName { get; }
    public string LastName { get; }
    public string SocialSecurityNumber { get; }

    // three-parameter constructor
    public Employee(string firstName, string lastName,
        string socialSecurityNumber)
    {
        FirstName = firstName;
        LastName = lastName;
        SocialSecurityNumber = socialSecurityNumber;
    }
```

Fig. 12.13 | Employee abstract base class that implements interface IPayment. (Part I of 2.)