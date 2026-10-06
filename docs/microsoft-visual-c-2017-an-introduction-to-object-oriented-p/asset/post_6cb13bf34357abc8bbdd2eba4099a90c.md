
## CHAPTER 10 Introduction to Inheritance

Figure 10-7 shows how you can declare salary as protected within the Employee class so that it becomes legal to access it directly within the CommissionRate set accessor of the CommissionEmployee derived class. Figure 10-8 contains a CommissionEmployee class.

```csharp
class Employee
{
    protected double salary;
    public int idNum {get; set;}
    public double Salary
    {
        get {
            return salary;
        }
        set {
            const double MIN = 15_000;
            if(value < MIN)
                salary = MIN;
            else
                salary = value;
        }
    }
    public string GetGreeting()
    {
        string greeting = "Hello. I am employee #" + idNum;
        return greeting;
    }
}
```

> Notice the salary field is protected.

**Figure 10-7** The Employee class with a protected field

```csharp
class CommissionEmployee : Employee
{
    private double commissionRate;
    public double CommissionRate
    {
        get {
            return commissionRate;
        }
        set {
            commissionRate = value;
            salary = 0;
        }
    }
}
```

> CommissionEmployee can use Employee's protected salary field.

**Figure 10-8** The CommissionEmployee class that uses its parent's protected field.

## Using the protected Access Specifier

that inherits from the new Employee class and uses the protected field. Figure 10-9 shows a program that instantiates a CommissionEmployee object, and Figure 10-10 shows the output. Notice that the CommissionEmployee's salary is initially set to 20,000 in the program, and the salary becomes 0 when the CommissionRate is set later.

**Figure 10-9** The DemoCommissionEmployee program.

| Salesperson #567: $60.00 per year |
| ...plus 6.00 % commission on all sales |

**Figure 10-10** Output of the DemoCommissionEmployee program.

If you set the salesperson's CommissionRate first in the DemoCommissionEmployee program, then set Salary to a nonzero value, the employee's salary will not be reduced to 0. Your intention is to always create CommissionEmployees with salaries of 0, then the salary should also be overridden in the derived class. You will learn about overriding parent class members in the next section.

Using the protected access specifier for a field can be convenient, and it slightly improves program performance by using a directly instead of "going through" property accessors. Also, using the protected access specifier is occasionally necessary. However, protected data members should be used sparingly. Whenever possible, the principle of information hiding should be observed, and even classes should go through accessors to "get to" their parent's data. When child classes are allowed direct access to a parent's fields, the likelihood of future errors increases. Classes that depend on name fields are fragile and are said to be fragile to errors—that is

## CHAPTER 10 Introduction to Inheritance

### TWO TRUTHS & A LIE
Using the protected Access Specifier

- 1. A child class does not contain the private members of its parent.
- 2. A child class cannot use the private members of its parent.
- 3. A child class can use the protected members of its parent, but outside classes cannot.

> The false statement is #1. A child class contains the private members of it, but cannot use them directly.

## Overriding Base Class Members

When you derive a derived class by extending an existing class, the new derived class contains properties and methods that were defined in the original base class. Sometimes, the superclass features are not entirely appropriate for the subclass objects. Using the same method or property name to indicate different implementations is called polymorphism. You first learned the term polymorphism in Chapter 1; it means "many forms". In programming, it means that many forms of action take place, even though you use the same name. Everyday provide examples of polymorphism:

- Both are instruments and have Play() method, guitar is played differently.
- Both are vehicles and have Operate() method, bicycle is operated differently.
- Both are schools and have Graduation() method, preschool is different. (Wait, let me re-align the OCR flow based on the provided text fragments).

In Chapter 9, you learned that a virtual method (or property) is one that can be overridden by a derived class. Suppose that you derive a subclass called Student, as shown in Figure 10-11. In Figure 10-11, the Credits property is declared with the override modifier (see shading) because it has the same header (that is, the same name and parameter list) as a property in its parent class. The Credits property overrides and hides its counterpart in the parent class. If you omit override, the program will still operate correctly, but you will receive a warning that you are hiding an inherited member with the same name in the base class. Using the keyword override eliminates the warning and makes your intentions clear. When you use the Name property with a CommissionEmployee object, a program uses the parent class Name; it is not hidden. When you use Credits to set a value for a CommissionEmployee object, the program uses the overriding property from its own class.

```csharp
class Student {
    private double RATE = 55;
    protected int credits;
    protected double tuition;
    public string Name {get; set;}
    public int Credits
    {
        get {
            return credits;
        }
        set {
            credits = value;
            tuition = value * RATE;
        }
    }
    public double Tuition {
        get {
            return tuition;
        }
    }
}
```

**Figure 10-11** The Student class.

Using the protected access specifier for a field can be convenient, and it slightly improves program performance by using a directly instead of "going through" property accessors. Also, using the protected access specifier is occasionally necessary. However, protected data members should be used sparingly. Whenever possible, the principle of information hiding should be observed, and even classes should go through accessors to "get to" their parent's data. When child classes are allowed direct access to a parent's fields, the likelihood of future errors increases. Classes that depend on name fields are fragile and are said to be fragile to errors—that is

```csharp
class CommissionEmployee : Student
{
    public override int Credits
    {
        set {
            credits = value;
            tuition = 0;
        }
    }
}
```
**Figure 10-12** The CommissionEmployee class.

(Note: The OCR text provided some jumbled fragments in the later pages 462-464. I have reconstructed the logical flow based on the technical context of C# inheritance provided.)
