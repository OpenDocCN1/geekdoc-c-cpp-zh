
# BEGINNER TOPIC

## Encapsulation Part 1: Objects Group Data with Methods

If you received a stack of index cards with employees' first names, a stack of index cards with their last names, and a stack of index cards with their salaries, the cards would be of little value unless you knew that the cards were in the same order in each stack. Even so, the data would be difficult to work with because determining a person's full name would require searching through two stacks. Worse, if you dropped one of the stacks, there would be no way to reassociate the first name with the last name and the salary. Instead, you would need one stack of employee cards in which the data for each employee is grouped on one card. With this approach, first names, last names, and salaries will be encapsulated together.

Outside the object-oriented programming context, to **encapsulate** a set of items is to enclose those items within a capsule. Similarly, object-oriented programming encapsulates methods and **data** together into an object. This provides a grouping of all of the class **members** (the data and methods within a class) so that they no longer need to be handled individually. Instead of passing a first name, a last name, and a salary as three separate parameters to a method, objects enable a call to pass a reference to an employee object. Once the called method receives the object reference, it can send a message (e.g., it can call a method such as `AdjustSalary()`) to the object to perform a particular operation.

## Language Contrast: C++—The delete Operator

C# programmers should view the **new** operator as a call to instantiate an object, not as a call to allocate memory. Both objects allocated on the heap and objects allocated on the stack support the **new** operator, emphasizing the point that **new** is not about how memory allocation should take place and whether de-allocation is necessary.

Thus C# does not need the **delete** operator found in C++. Memory allocation and de-allocation are details that the runtime manages, allowing the developer to focus more on domain logic. However, though memory is managed by the runtime, the runtime does not manage other resources such as database connections, network ports, and so on. Unlike C++, C# does not support **implicit deterministic resource cleanup** (the occurrence of implicit object destruction at a compile-time-defined location in the code). Fortunately, C# does support **explicit deterministic resource cleanup** via a **using** statement and **implicit nondeterministic resource cleanup** using **finalizers**.

## Instance Fields

One of the key aspects of object-oriented design is the grouping of data to provide structure. This section discusses how to add data to the Employee class. The general object-oriented term for a variable that stores data within a class is member variable. This term is well understood in C#, but the more standard term and the one used in the specification is field, which is a named unit of storage associated with the containing type. Instance fields are variables declared at the class level to store data associated with an object. Hence, association is the relationship between the field data type and the containing field.

### Declaring an Instance Field

In Listing 6.4, the class Employee has been modified to include three fields: FirstName, LastName, and Salary.

**LISTING 6.4: Declaring Fields**

```csharp
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary;
}
```

With these fields added, it is possible to store some fundamental data with every Employee instance. In this case, you prefix the fields with an access modifier of public. The use of public on a field indicates that the data within the field is accessible from classes other than Employee (see the section “Access Modifiers” later in this chapter).

As with local variable declarations, a field declaration includes the data type to which the field refers. Furthermore, it is possible to assign fields an initial value at declaration time, as demonstrated with the Salary field in Listing 6.5.

**LISTING 6.5: Setting Initial Values of Fields at Declaration Time**

```csharp
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary = "Not enough";
}
```

We delay the guidelines of naming and coding fields until later in the chapter, after C# properties have been introduced. Suffice it to say, Listing 6.5 does *not* follow the general convention.

### Accessing an Instance Field

You can set and retrieve the data within fields. However, the fact that a field does not include a static modifier indicates that it is an instance field. You can access an instance field only from an instance of the containing class (an object). You cannot access it from the class directly (without first creating an instance, in other words).

Listing 6.6 shows an updated look at the Program class and its utilization of the Employee class, and Output 6.1 shows the results.

**LISTING 6.6: Accessing Fields**

```csharp
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        Employee employee2;
        employee2 = new Employee();

        employee1.FirstName = "Inigo";
        employee1.LastName = "Montoya";
        employee1.Salary = "Too Little";
        IncreaseSalary(employee1);
        Console.WriteLine(
            "{0} {1}: {2}",
            employee1.FirstName,
            employee1.LastName,
            employee1.Salary);
        // ...
    }

    static void IncreaseSalary(Employee employee)
    {
        employee.Salary = "Enough to survive on";
    }
}
```

**OUTPUT 6.1**

```text
Inigo Montoya: Enough to survive on
```

Listing 6.6 instantiates two Employee objects, as you saw earlier. It then sets each field, calls `IncreaseSalary()` to change the salary, and displays each field associated with the object referenced by `employee1`.

Notice that you first have to specify which Employee instance you are working with. Therefore, the `employee1` variable appears as a prefix to the field name when assigning and accessing the field.

## Instance Methods

One alternative to formatting the names in the WriteLine() method call within Main() is to provide a method in the Employee class that takes care of the formatting. Changing the functionality to be within the Employee class rather than a member of Program is consistent with the encapsulation of a class. Why not group the methods relating to the employee’s full name with the class that contains the data that forms the name?

Listing 6.7 demonstrates the creation of such a method.

**LISTING 6.7: Accessing Fields from within the Containing Class**

```csharp
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary;

    public string GetName()
    {
        return $"{ FirstName } { LastName }";
    }
}
```

There is nothing particularly special about this method compared to what you learned in Chapter 4, except that now the GetName() method accesses fields on the object instead of just local variables. In addition, the method declaration is not marked with static. As you will see later in this chapter, static methods cannot directly access instance fields within a class. Instead, it is necessary to obtain an instance of the class to call any instance member, whether a method or a field.

Given the addition of the GetName() method, you can update Program.Main() to use the method, as shown in Listing 6.8 and Output 6.2.

**LISTING 6.8: Accessing Fields from outside the Containing Class**

```csharp
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        Employee employee2;
        employee2 = new Employee();

        employee1.FirstName = "Inigo";
        employee1.LastName = "Montoya";
        employee1.Salary = "Too Little";
        IncreaseSalary(employee1);
        Console.WriteLine(
            $"{ employee1.GetName() }:{ employee1.Salary }");

        // ...
    }
    // ...
}
```

**OUTPUT 6.2**

```text
Inigo Montoya: Enough to survive on
```

## Using the this Keyword

You can obtain the reference to a class from within instance members that belong to the class. To indicate explicitly that the field or method accessed is an instance member of the containing class in C#, you use the keyword this. Use of this is implicit when calling any instance member, and it returns an instance of the object itself.

For example, consider the SetName() method shown in Listing 6.9.

**LISTING 6.9: Using this to Identify the Field's Owner Explicitly**

```csharp
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary;

    public string GetName()
    {
        return $"{ FirstName } { LastName }";
    }
}
```
