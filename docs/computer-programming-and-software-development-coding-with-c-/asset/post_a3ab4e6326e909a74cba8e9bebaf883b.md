
```
namespace System
{
    public interface ICloneable
    {
        object Clone();
    }
}
```

Most of these interfaces are very simple. As you can see here, for example, the ICloneable. The interface just defines a method Clone that we need to implement. When then somewhere else a clone of an object implementing this interface is invoked, our code will be invoked. Let's return to Visual Studio and implement one of these commonly used interfaces, IComparable. Then I'll show you what extra behavior we are getting by implementing this interface. I have changed the Employee class again slightly.

```
public class Employee: IEmployee
{
    private int id;
    private string firstName;
    private string lastName;
    private string email;

    private int numberOfHoursWorked;
    private double wage;
    private double? hourlyRate;
    public static double taxRate = 0.15;

    private DateTime birthDay;

    public int Id
    {
        get { return id; }
        set
        {
            id = value;
        }
    }

    public string FirstName
    {
        get { return firstName; }
        set
        {
            firstName = value;
        }
    }
```

I've added the id filter and an id property. What I now want to do is I want to enable sorting. When I give a list of employees, I want to be able to sort them based on the value of this id. C#, or, in fact, I should say .NET, comes with quite a few interfaces, and one of them is the IComparable interface. The IComparable interface comes with the CompareTo method. In this method, I can write logic to compare the current object with another object. I need to write my own logic in that method.

```
public void DisplayEmployeeDetails()
{
    Console.WriteLine($"\nFirst name: {FirstName}\nLast name: {LastName}\nEmail: {Email}\nBirthday: {BirthDay.ToShortDateString()}\n");
}

public virtual void GiveBonus()
{
    Console.WriteLine($"{FirstName} {LastName} received a generic bonus of 100!");
}

public void GiveCompliment()
{
    Console.WriteLine($"You've done a great job, {FirstName}");
}

public int CompareTo(object obj)
{
    var otherEmployee = (Employee)obj;
    if (Id > otherEmployee.Id)
        return 1;
    else if (Id < otherEmployee.Id)
        return -1;
    else
        return 0;
}
```

I am implementing the contract, and that can then be used by C# to compare two objects. I'm going to go back to my Employee class, and I'm going to implement the IComparable interface. The IComparable interface, as mentioned, has one method, the CompareTo method, and I've asked Visual Studio to generate it. In this CompareTo method, I'm now going to write logic to compare my current object with the object that is being passed in as a parameter here. Let me add that now. I'm writing logic here to compare the current employee with another object, but I'm going to assume that that is also an employee. So I'm going to cast that object into an employee, and then I'm going to compare the id values. I'm going to check if the id is larger than the one that's being passed in, then I return 1. If it's less than, I return and if they're the same, I return 0. This +1, or 0 is actually a sign for C# to understand whether or not the object being passed in is large or small. Those values it knows, so I need to provide a logic to come to that +1, or 0. Now

by making my employee implement the IComparable and providing the CompareTo method, I've signed the contract that my type can actually be sorted, and that, well, opens doors. Let me show you the Program class now.

```
class Program
{
    static void Main(string[] args)
    {
        Employee bethany = new StoreManager(55156, "Bethany", "Smith", "bethany@snowball.be", new DateTime(1979, 1, 16), 25);
        Manager mary = new Manager(748, "Mary", "Jones", "mary@snowball.be", new DateTime(1965, 1, 16), 30);
        JuniorResearcher bobJunior = new JuniorResearcher(11231, "Bob", "Spencer", "bob@snowball.be", new DateTime(1988, 1, 23), 17);
        Employee kevin = new StoreManager(81131, "Kevin", "Marks", "kevin@snowball.be", new DateTime(1953, 12, 12), 10);
        Employee kate = new StoreManager(100, "Kate", "Greggs", "kate@snowball.be", new DateTime(1993, 8, 8), 10);

        List<Employee> employees = new List<Employee>();
        employees.Add(bethany);
        employees.Add(mary);
        employees.Add(bobJunior);
        employees.Add(kevin);
        employees.Add(kate);

        employees.Sort();

        foreach (var employee in employees)
        {
            employee.DisplayEmployeeDetails();
        }

        Console.ReadLine();
    }
}
```

I've changed it slightly so that in the constructor of the StoreManager, the Manager, and so on, I now also pass in the id. Let's take a look at the Manager constructor. That now comes with an id parameter because the base constructor, the one on Employee, also now comes with an Employee id. I've defined a few employees, and I've now placed them here in this list.

```
public class Manager : Employee
{
    public Manager(int id, string first, string last, string em, DateTime bd, double? rate) : base(id, first, last, em, bd, rate)
    {
    }

    public void AttendManagementMeeting()
    {
        NumberOfHoursWorked += 10;

        Console.WriteLine($"Manager {FirstName} {LastName} is now attending a long meeting that could have been an email!");
    }

    public override void GiveBonus()
    {
        if (NumberOfHoursWorked > 5)
            Console.WriteLine($"Manager {FirstName} {LastName} received a management bonus of 500!");
        else
            Console.WriteLine($"Manager {FirstName} {LastName} received a management bonus of 250!");
    }
}
```

This is a generic list, and that has the ability to sort. If I ask C# to sort a list of employees, it doesn't know how to do that. It doesn't know if I want to sort them by first name, by last name, hence, I have on my Employee type implemented the IComparable, and I've provided my own comparison logic.

```
List<Employee> employees = new List<Employee>();
employees.Add(bethany);
employees.Add(mary);
employees.Add(bobJunior);
employees.Add(kevin);
employees.Add(kate);

employees.Sort();

foreach (var employee in employees)
{
    employee.DisplayEmployeeDetails();
}

Console.ReadLine();
```

I have, in other words, signed the contract that my type knows how to be sorted. That's why interfaces are important. So, calling the Sort

method on the list of employees will invoke the CompareTo method to sort my list.

```
public int CompareTo(object obj)
{
    var otherEmployee = (Employee)obj;
    if (Id > otherEmployee.Id)
        return 1;
    else if (Id < otherEmployee.Id)
        return -1;
    else
        return 0;
}
```

Let's put a breakpoint in the Employee CompareTo, and then we'll see that this CompareTo method is automatically invoked when the Sort method is running on my list. It's called a few times to sort all the items, and once it's done sorting, we will see that employee 1 is the 1 with id 100, that's the lowest id, the second one is 748, and the 1 here, the last in the list, has the highest id. So indeed, the sorting worked based on the ids. By implementing the IComparable interface and providing my own CompareTo method, I signed a contract saying that I define a method to specify how sorting needs to work. Interfaces can be used to enforce that types implement certain numbers. In the very final part of this book, I want to show you how interfaces relate to polymorphism. By working with interfaces, say the IEmployee interface, we're also creating a relation between the interface and the type implementing the interface. Just like with inheritance, an relation is established when implementing the interface.

```
IEmployee e1 = new Manager();

e1.PerformWork();
```

Although we can't instantiate interface types, the code you see here on the screenshot is perfectly valid. I'm using a variable, which has the IEmployee type, so the interface. But through polymorphic behavior, we can use this to point to anything that implements the IEmployee interface. And to top it off, we can on that instance call methods that are defined in the contract, that would here be the PerformWork. In the last demonstration of this book, let's take another look at the polymorphic behavior of interfaces in C#.
Interfaces also provide polymorphic behavior. Because of the fact that Employee implements the IEmployee interface, every employee, but also every Manager, every Researcher is an IEmployee. So if I go back to the program class, I can, everywhere where I used Employee, also use IEmployee. Every StoreManager is, as said, an IEmployee, so is every Manager, so is every JuniorResearcher, as well as every StoreManager. So because of the fact that the base type, Employee, implements the IEmployee interface, every Manager is also an IEmployee and can be addressed as such. I do get an exception here because my Employee list here is expecting employees.

```
static void Main(string[] args)
{
    IEmployee bethany = new StoreManager(55156, "Bethany", "Smith", "bethany@snowball.be", new DateTime(1979, 1, 16), 25);
    IEmployee mary = new Manager(748, "Mary", "Jones", "mary@snowball.be", new DateTime(1965, 1, 16), 30);
    IEmployee bobJunior = new JuniorResearcher(11231, "Bob", "Spencer", "bob@snowball.be", new DateTime(1988, 1, 23), 17);
    IEmployee kevin = new StoreManager(81131, "Kevin", "Marks", "kevin@snowball.be", new DateTime(1953, 12, 12), 10);
    IEmployee kate = new StoreManager(100, "Kate", "Greggs", "kate@snowball.be", new DateTime(1993, 8, 8), 10);

    List<Employee> employees = new List<Employee>();
    employees.Add(bethany);
    employees.Add(mary);
    employees.Add(bobJunior);
    employees.Add(kevin);
    employees.Add(kate);

    employees.Sort();

    foreach (var employee in employees)
    {
        employee.DisplayEmployeeDetails();
    }

    Console.ReadLine();
}
```
