
It needs to point to its direct parent, and this we can do by adding behind the class name a colon, and then the name of the BaseClass. The colon, and then the BaseClass name, are the way to create inheritance in C#. Doing this has quite a few consequences, as you'll come to understand. When we apply this on our business case, Employee will be the BaseClass, and we don't need to make any changes to that class at this point. Then, we'll bring in another class, Manager, and that will inherit from Employee.

```
public class Employee
{

}
```

It has a colon and then Employee as its base type. Manager is now the DerivedClass, and Employee is the BaseClass. As said, introducing a BaseClass has a number of consequences, which is pretty much why we would add inheritance.

```
public class Manager: Employee
{

}
```

The Employee class will contain a functionality that all inherited types will gain because of inheriting from it. This means that the name field and the PerformWork method here, defined on Employee, will become available for Manager, as if they were part of Manager directly. That is what you see here. Manager itself now contains a method called DisplayManagerData, which for now will just display the name of the manager. But notice that Manager doesn't contain the name field. No, it is defined on Employee.

```
public class Employee
{
    public string name;
    public void PerformWork()
    {
    }
}
```

```
public class Manager: Employee
{
    public void DisplayManagerData()
    {
        Console.WriteLine(name);
    }
}
```

But we can use it on Manager because we inherit from Employee. Members defined on the BaseClass will now become accessible for the DerivedClass. Now, that last sentence does require some extra explanation. The DerivedClass can access some members of the BaseClass. This is where access modifiers start playing an important role. Remember the three most important modifiers. Public and private we've already looked at briefly, and there's that other one, protected. When using inheritance, the DerivedClass can access the public members from the parent. No questions asked. However, members defined as private on the BaseClass are not accessible, they are internal to the class, and can't even be accessed by inheriting types. So if you want the DerivedClass never to access a certain field, property, or method, just make it private in the BaseClass. Protected is somewhat in the middle. When using inheritance, protected members of the BaseClass are accessible from the inheriting type. So, for a DerivedClass, public and protected mean the same. They can access protected members just like they would access public members. However, protected members cannot be accessed from anywhere else. So for types, protected members are private. Let's see these access modifiers in action before we head back to Visual Studio. Notice now that I have made name private on the Employee. Private means mine and mine only. No one can see or use this member. Our trusted Manager class, although it inherits

from Employee, now won't be able to access the name field any longer. You'll even get a compile error saying that, indeed, name is private and cannot be accessed from a DerivedClass. However, making name protected again does allow the Manager class to access it. Protected behaves like public for inheriting types. For anything else, it behaves like private, so the member will not be accessible. We've been talking for quite a while now about inheritance. Time to see it in action. Let's head back to Visual Studio and see how we can turn our employee into a base class. Then, we'll create an inheriting class, and finally, we'll learn about the access modifiers and what influence they have. So far, we've used the employeeType variable and the EmployeeType property to distinguish between the different types an employee could be.

```
```csharp
public enum EmployeeType
{
    Sales,
    Manager,
    Research,
    StoreManager
}
```
```

And we used for that the EmployeeType enumeration. But now in this demonstration, we're going to introduce, well, different types, different classes, really, to represent the different types of employee such as a manager, a salesperson, and so on. So, I'm going to refactor my class first. Refactoring means, well, changing things a bit so that I don't need that employeeType variable anymore. That is going to give me some errors.

```
public Employee(string first, string last, string em, DateTime bd, double? rate)
{
    FirstName = first;
    LastName = last;
    Email = em;
    BirthDay = bd;
    HourlyRate = rate ?? 10;
}

public void PerformWork()
{
    NumberOfHoursWorked++;
    Console.WriteLine($"{FirstName} {LastName} is now working!");
}

public void StopWorking()
{
    Console.WriteLine($"{FirstName} {LastName} has stopped working!");
}

public double ReceiveWage()
{
    double wageBeforeTax = NumberOfHoursWorked * HourlyRate.Value;
    double taxAmount = wageBeforeTax * taxRate;
    Wage = wageBeforeTax - taxAmount;
```

As you can see here, I'm also going to have to remove the EmployeeType here, and I'm also going to remove that here from the constructor. And finally, I'm going to also remove it here. I seem to be having another error in date inside of the DisplayEmployeeDetails. I also need to remove this reference to the EmployeeType property as well.

```
public void DisplayEmployeeDetails()
{
    Console.WriteLine($"\nFirst name: {FirstName}\nLast name: {LastName}\nEmail: {Email}\nBirthday: {BirthDay.ToShortDateString()}\n");
}

public enum EmployeeType
{
    Sales,
    Manager,
    Research,
    StoreManager
}
```

Visual Studio now says that the EmployeeType enumeration, well, isn't used anymore, so I can actually remove this, and then things should compile fine. So I'm now at the point where I have my Employee class, and I'm going to represent different types of employees through different classes. And for that, I'm going to use inheritance. So, inside of this HR folder, I'm going to add a new class, and that's going to be the Manager. In fact, the manager is very similar to an employee. A lot of the functionalities that we have defined so far such as the hourlyRate, the firstName, but also the methods such as PerformWork, ReceiveWage, StopWorking, well, they also apply for a manager. That is why I'm going to introduce inheritance here. I'm going to let the Manager class inherit from the Employee class. I'm going to do that by writing a colon and then the name of the base class. I'm also going to make this class public.

![](img/0155736aec718cf18821e9f10a5d308d_825_0.png)

Visual Studio now does throw a small error here, saying that there is no argument given that corresponds to the required formal parameter 'first' of Employee.Employee and then a couple of types. That's a bit of a confusing error. But if you look here, this actually points to the constructor, indeed. What I need to do is I also need to provide in my Manager type a constructor that will then pass data to the base constructor because I can, in fact, not create a manager without there being an employee, really, because every manager is, in fact, an employee. So I'm going to introduce a constructor here, and we do that as we did before. It's going to consist out of the access

modifier public and the name of the class. I'm also going to be passing in a couple of parameters, Let me add those first, and let's introduce again curly braces.

```
```csharp
{
    public class Manager: Employee
    {
        public Manager(string first, string last, string em, DateTime bd, double? rate)
        {
        }
    }
}
```
```

There's still an error that is, again, saying pretty much the same. It is still saying we need to create an employee before we have that manager. So I need to, in fact, invoke the base constructor, and that's going to happen through the base keyword. The base keyword allows me to, call the base constructor, passing in values that are now passed in for the manager to the base type. So I can now, in fact, here say call the base constructor to the one on Employee, passing in the value, first, so that's this one, and I'm going to pass that to the base, so the Employee constructor. I'm going to do the same for last. I'm going to do the same for em. I'm going to do the same for bd, the birth date that was, and I'm also going to be passing in a rate. And now Visual Studio is happy, as you can see. It's now accepting my change. So what I've now basically done to introducing the base keyword is calling the constructor on the base class, so on the employee, passing in the values passed in for my manager creation.
