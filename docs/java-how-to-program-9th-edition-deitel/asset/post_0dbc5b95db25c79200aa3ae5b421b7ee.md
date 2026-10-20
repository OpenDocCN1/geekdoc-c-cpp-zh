
Not every class relationship is an inheritance relationship. In Chapter 8, we discussed the has-a relationship, in which classes have members that are references to objects of other classes. Such relationships create classes by composition of existing classes. For example, given the classes Employee, BirthDate and TelephoneNumber, it’s improper to say that an Employee is a BirthDate or that an Employee is a TelephoneNumber. However, an Employee has a BirthDate, and an Employee has a TelephoneNumber.

It’s possible to treat superclass objects and subclass objects similarly—their commonalities are expressed in the superclass’s members. Objects of all classes that extend a common superclass can be treated as objects of that superclass—such objects have an is-a relationship with the superclass. Later in this chapter and in Chapter 10, we consider many examples that take advantage of the is-a relationship.

A subclass can customize methods that it inherits from its superclass. To do this, the subclass overrides (redefines) the superclass method with an appropriate implementation, as we’ll see often in the chapter’s code examples.

## 9.3 protected Members

Chapter 8 discussed access modifiers public and private. A class’s public members are accessible wherever the program has a reference to an object of that class or one of its subclasses. A class’s private members are accessible only within the class itself. In this section, we introduce access modifier protected. Using protected access offers an intermediate level of access between public and private. A superclass’s protected members can be accessed by members of that superclass, by members of its subclasses and by members of other classes in the same package—protected members also have package access.

All public and protected superclass members retain their original access modifier when they become members of the subclass—public members of the superclass become public members of the subclass, and protected members of the superclass become protected members of the subclass. A superclass’s private members are not accessible outside the class itself. Rather, they’re hidden in its subclasses and can be accessed only through the public or protected methods inherited from the superclass.

Subclass methods can refer to public and protected members inherited from the superclass simply by using the member names. When a subclass method overrides an inherited superclass method, the superclass method can be accessed from the subclass by preceding the superclass method name with keyword super and a dot (.) separator. We discuss accessing overridden members of the superclass in Section 9.4.

> Software Engineering Observation 9.1
> Methods of a subclass cannot directly access private members of their superclass. A subclass can change the state of private superclass instance variables only through non-private methods provided in the superclass and inherited by the subclass.

> Software Engineering Observation 9.2
> Declaring private instance variables helps you test, debug and correctly modify systems. If a subclass could access its superclass’s private instance variables, classes that inherit from that subclass could access the instance variables as well. This would propagate access to what should be private instance variables, and the benefits of information hiding would be lost.

## 9.4 Relationship between Superclasses and Subclasses

We now use an inheritance hierarchy containing types of employees in a company’s payroll application to discuss the relationship between a superclass and its subclass. In this company, commission employees (who will be represented as objects of a superclass) are paid a percentage of their sales, while base-salaried commission employees (who will be represented as objects of a subclass) receive a base salary plus a percentage of their sales.

We divide our discussion of the relationship between these classes into five examples. The first declares class CommissionEmployee, which directly inherits from class Object and declares as private instance variables a first name, last name, social security number, commission rate and gross (i.e., total) sales amount.

The second example declares class BasePlusCommissionEmployee, which also directly inherits from class Object and declares as private instance variables a first name, last name, social security number, commission rate, gross sales amount and base salary. We create this class by writing every line of code the class requires—we’ll soon see that it’s much more efficient to create it by inheriting from class CommissionEmployee.

The third example declares a new BasePlusCommissionEmployee class that extends class CommissionEmployee (i.e., a BasePlusCommissionEmployee is a CommissionEmployee who also has a base salary). This software reuse lets us write less code when developing the new subclass. In this example, class BasePlusCommissionEmployee attempts to access class CommissionEmployee’s private members—this results in compilation errors, because the subclass cannot access the superclass’s private instance variables.

The fourth example shows that if CommissionEmployee’s instance variables are declared as protected, the BasePlusCommissionEmployee subclass can access that data directly. Both BasePlusCommissionEmployee classes contain identical functionality, but we show how the inherited version is easier to create and manage.

After we discuss the convenience of using protected instance variables, we create the fifth example, which sets the CommissionEmployee instance variables back to private to enforce good software engineering. Then we show how the BasePlusCommissionEmployee subclass can use CommissionEmployee’s public methods to manipulate (in a controlled manner) the private instance variables inherited from CommissionEmployee.

### 9.4.1 Creating and Using a CommissionEmployee Class

We begin by declaring class CommissionEmployee (Fig. 9.4). Line 4 begins the class declaration and indicates that class CommissionEmployee extends (i.e., inherits from) class Object (from package java.lang). This causes class CommissionEmployee to inherit the class Object’s methods—class Object does not have any fields. If you don’t explicitly specify which class a new class extends, the class extends Object implicitly. For this reason, you typically will not include “extends Object” in your code—we do so in this example only for demonstration purposes.

### Overview of Class CommissionEmployee’s Methods and Instance Variables

Class CommissionEmployee’s public services include a constructor (lines 13–22) and methods earnings (lines 93–96) and toString (lines 99–107). Lines 25–90 declare public get and set methods for the class’s instance variables (declared in lines 6–10) firstName, lastName, socialSecurityNumber, grossSales and commissionRate. The class declares its instance variables as private, so objects of other classes cannot directly access

these variables. Declaring instance variables as private and providing get and set methods to manipulate and validate them helps enforce good software engineering. Methods setGrossSales and setCommissionRate, for example, validate their arguments before assigning the values to instance variables grossSales and commissionRate. In a real-world, business-critical application, we’d also perform validation in the class’s other set methods.

// Fig. 9.4: CommissionEmployee.java
// CommissionEmployee class represents an employee paid a
// percentage of gross sales.
public class CommissionEmployee extends Object
{
    private String firstName;
    private String lastName;
    private String socialSecurityNumber;
    private double grossSales; // gross weekly sales
    private double commissionRate; // commission percentage

    // five-argument constructor
    public CommissionEmployee( String first, String last, String ssn,
        double sales, double rate )
    {
        // implicit call to Object constructor occurs here
        firstName = first;
        lastName = last;
        socialSecurityNumber = ssn;
        setGrossSales( sales ); // validate and store gross sales
        setCommissionRate( rate ); // validate and store commission rate
    } // end five-argument CommissionEmployee constructor

    // set first name
    public void setFirstName( String first )
    {
        firstName = first; // should validate
    } // end method setFirstName

    // return first name
    public String getFirstName()
    {
        return firstName;
    } // end method getFirstName

    // set last name
    public void setLastName( String last )
    {
        lastName = last; // should validate
    } // end method setLastName

    // return last name
    public String getLastName()
    {
```

Fig. 9.4 | CommissionEmployee class represents an employee paid a percentage of gross sales. (Part 1 of 3.)
