
## LISTING 10.3

```java
//***************************************************************************
// StaffMember.java      Author: Lewis/Loftus
//
// Represents a generic staff member.
//***************************************************************************

abstract public class StaffMember
{
    protected String name;
    protected String address;
    protected String phone;

    //-------------------------------------------------------------
    // Constructor: Sets up this staff member using the specified
    // information.
    //-------------------------------------------------------------
    public StaffMember (String eName, String eAddress, String ePhone)
    {
        name = eName;
        address = eAddress;
        phone = ePhone;
    }

    //-------------------------------------------------------------
    // Returns a string including the basic employee information.
    //-------------------------------------------------------------
    public String toString()
    {
        String result = "Name: " + name + "\n";

        result += "Address: " + address + "\n";
        result += "Phone: " + phone;

        return result;
    }

    //-------------------------------------------------------------
    // Derived classes must define the pay method for each type of
    // employee.
    //-------------------------------------------------------------
    public abstract double pay();
}
```

## CHAPTER 10 Polymorphism

However, the descendants of StaffMember each provide their own specific definition for pay. By defining pay abstractly in StaffMember, the payday method of StaffMember can polymorphically pay each employee.

This is the essence of polymorphism. Each class knows best how it should handle a specific behavior, in this case paying an employee. Yet in one sense it’s all the same behavior—the employee is getting paid. Polymorphism lets us treat similar objects in consistent but unique ways.

The Volunteer class shown in Listing 10.4 represents a person that is not compensated monetarily for his or her work. We keep track only of a volunteer’s basic information, which is passed into the constructor of the Volunteer, which in turn passes it to the StaffMember constructor using the super reference. The pay method of Volunteer simply returns a zero pay value.

## LISTING 10.4

```java
// Volunteer.java
// Author: Lewis/Loftus
// Represents a staff member that works as a volunteer.
public class Volunteer extends StaffMember
{
    // Constructor: Sets up this volunteer using the specified
    // information.
    public Volunteer (String eName, String eAddress, String ePhone)
    {
        super (eName, eAddress, ePhone);
    }

    // Returns a zero pay value for this volunteer.
    public double pay()
    {
        return 0.0;
    }
}
```

If pay had not been overridden, the Volunteer class would have been considered abstract and could not have been instantiated.

Note that when a volunteer gets “paid” in the payday method of Staff, a simple expression of thanks is printed. In all other situations, where the pay value is greater than zero, the payment itself is printed.

The Employee class shown in Listing 10.5 represents an employee that gets paid at a particular rate each pay period. The pay rate, as well as the employee’s Social Security number, is passed along with the other basic information to the Employee constructor. The basic information is passed to the constructor of StaffMember using the super reference.

The toString method of Employee is overridden to concatenate the additional information that Employee manages to the information returned by the parent’s version of toString, which is called using the super reference. The pay method of an Employee simply returns the pay rate for that employee.

The Executive class shown in Listing 10.6 represents an employee that may earn a bonus in addition to his or her normal pay rate. The Executive class is derived from Employee and therefore inherits from both StaffMember and Employee. The constructor of Executive passes along its information to the Employee constructor and sets the executive bonus to zero.

A bonus is awarded to an executive using the awardBonus method. This method is called in the Staff constructor for the only executive that is part of the staffList array. Note that the generic StaffMember reference must be cast into an Executive reference to invoke the awardBonus method (which doesn’t exist for a StaffMember).

The Executive class overrides the pay method so that it first determines the payment as it would for any employee, then adds the bonus. The pay method of the Employee class is invoked using super to obtain the normal payment amount. This technique is better than using just the payRate variable, because if we choose to change how Employee objects get paid, the change will automatically be reflected in Executive. After the bonus is awarded, it is reset to zero.

The Hourly class shown in Listing 10.7 represents an employee whose pay rate is applied on an hourly basis. It keeps track of the number of hours worked in the current pay period, which can be modified by calls to the addHours method. This method is called from the payday method of Staff. The pay method of Hourly determines the payment based on the number of hours worked and then resets the hours to zero.

## LISTING 10.5

```java
//******************************
// Employee.java      Author: Lewis/Loftus
// Represents a general paid employee.
//******************************

public class Employee extends StaffMember
{
    protected String socialSecurityNumber;
    protected double payRate;

    //-------------------------------------------------------------
    // Constructor: Sets up this employee with the specified information.
    //-------------------------------------------------------------
    public Employee (String eName, String eAddress, String ePhone,
                     String socSecNumber, double rate)
    {
        super (eName, eAddress, ePhone);
        socialSecurityNumber = socSecNumber;
        payRate = rate;
    }

    //-------------------------------------------------------------
    // Returns information about an employee as a string.
    //-------------------------------------------------------------
    public String toString()
    {
        String result = super.toString();
        result += "\nSocial Security Number: " + socialSecurityNumber;
        return result;
    }

    //-------------------------------------------------------------
    // Returns the pay rate for this employee.
    //-------------------------------------------------------------
    public double pay()
    {
        return payRate;
    }
}
```

## LISTING 10.6

```java
//************************************************************************
// Executive.java      Author: Lewis/Loftus
//
// Represents an executive staff member, who can earn a bonus.
//************************************************************************

public class Executive extends Employee
{
    private double bonus;

    //-------------------------------------------------------------
    // Constructor: Sets up this executive with the specified
    // information.
    //-------------------------------------------------------------
    public Executive (String eName, String eAddress, String ePhone,
                      String socSecNumber, double rate)
    {
        super (eName, eAddress, ePhone, socSecNumber, rate);

        bonus = 0;  // bonus has yet to be awarded
    }

    //-------------------------------------------------------------
    // Awards the specified bonus to this executive.
    //-------------------------------------------------------------
    public void awardBonus (double execBonus)
    {
        bonus = execBonus;
    }

    //-------------------------------------------------------------
    // Computes and returns the pay for an executive, which is the
    // regular employee payment plus a one-time bonus.
    //-------------------------------------------------------------
    public double pay()
    {
        double payment = super.pay() + bonus;

        bonus = 0;

        return payment;
    }
}
```

## LISTING 10.7

```java
//***************************************************************************
// Hourly.java      Author: Lewis/Loftus
//
// Represents an employee that gets paid by the hour.
//***************************************************************************

public class Hourly extends Employee
{
    private int hoursWorked;

    //-------------------------------------------------------------
    // Constructor: Sets up this hourly employee using the specified
    // information.
    //-------------------------------------------------------------
    public Hourly (String eName, String eAddress, String ePhone,
                   String socSecNumber, double rate)
    {
        super (eName, eAddress, ePhone, socSecNumber, rate);

        hoursWorked = 0;
    }

    //-------------------------------------------------------------
    // Adds the specified number of hours to this employee's
    // accumulated hours.
    //-------------------------------------------------------------
    public void addHours (int moreHours)
    {
        hoursWorked += moreHours;
    }

    //-------------------------------------------------------------
    // Computes and returns the pay for this hourly employee.
    //-------------------------------------------------------------
    public double pay()
    {
        double payment = payRate * hoursWorked;

        hoursWorked = 0;

        return payment;
    }
}
```
