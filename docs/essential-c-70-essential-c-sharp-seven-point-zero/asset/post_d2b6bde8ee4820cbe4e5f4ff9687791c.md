
circle contains all patents. The intersection includes both inventors and patents, and a line is formed for each case where there is a match of inventors to patents. As the diagram shows, each inventor may have multiple patents and each patent can have one or more inventors. Each patent has an inventor, but in some cases inventors do not yet have patents.

![](img/ef6a8a417630b222bfb3f3b949facff0_665_0.png)

# FIGURE 15.3: Venn Diagram of Inventor and Patent Collections

Matching up inventors within the intersection to patents is an inner join. The result is a collection of inventor/patent pairs in which both patents and inventions exist for a pair. A left outer join includes all the items within the left circle regardless of whether they have a corresponding patent. In this particular example, a right outer join would be the same as an inner join because there are no patents without inventors. Furthermore, the designation of left versus right is arbitrary, so there is really no distinction between left and right outer joins. A full outer join, however, would include records from both outer sides; it is relatively rare to perform a full outer join.

Another important characteristic in the relationship between inventors and patents is that it is a many-to-many relationship. Each individual patent can have one or more inventors (e.g., the flying machine’s invention by both Orville and Wilbur Wright). Furthermore, each inventor can have one or more patents (e.g., Benjamin Franklin’s invention of both bifocals and the phonograph).

Another common relationship is a **one-to-many** relationship. For example, a company department may have many employees. However, each employee can belong to only one department at a time. (However, as is common with one-to-many relationships, adding the factor of time can transform them into many-to-many relationships. A particular employee may move from one department to another so that, over time, she could potentially be associated with multiple departments, making another many-to-many relationship.)

Listing 15.18 provides a sample listing of employee and department data, and Output 15.6 shows the results.

**LISTING 15.18: Sample Employee and Department Data**

```csharp
public class Department
{
    public long Id { get; set; }
    public string Name { get; set; }
    public override string ToString()
    {
        return Name;
    }
}

public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Title { get; set; }
    public int DepartmentId { get; set; }
    public override string ToString()
    {
        return $"{ Name } ({ Title })";
    }
}

public static class CorporateData
{
    public static readonly Department[] Departments =
        new Department[]
        {
            new Department(){
                Name="Corporate", Id=0},
            new Department(){
                Name="Human Resources", Id=1},
            new Department(){
                Name="Engineering", Id=2},
            new Department(){
                Name="Information Technology",
                Id=3},
            new Department(){
                Name="Philanthropy",
                Id=4},
            new Department(){
                Name="Marketing",
                Id=5},
        };

    public static readonly Employee[] Employees = new Employee[]
    {
        new Employee(){
            Name="Mark Michaelis",
            Title="Chief Computer Nerd",
            DepartmentId = 0},
        new Employee(){
            Name="Michael Stokesbury",
            Title="Senior Computer Wizard",
            DepartmentId=2},
        new Employee(){
            Name="Brian Jones",
            Title="Enterprise Integration Guru",
            DepartmentId=2},
        new Employee(){
            Name="Anne Beard",
            Title="HR Director",
            DepartmentId=1},
        new Employee(){
            Name="Pat Dever",
            Title="Enterprise Architect",
            DepartmentId = 3},
        new Employee(){
            Name="Kevin Bost",
            Title="Programmer Extraordinaire",
            DepartmentId = 2},
        new Employee(){
            Name="Thomas Heavey",
            Title="Software Architect",
            DepartmentId = 2},
        new Employee(){
            Name="Eric Edmonds",
            Title="Philanthropy Coordinator",
            DepartmentId = 4}}
};

class Program
{
    static void Main()
    {
        IEnumerable<Department> departments =
            CorporateData.Departments;
        Print(departments);

        Console.WriteLine();

        IEnumerable<Employee> employees =
            CorporateData.Employees;
        Print(employees);
    }

    private static void Print<T>(IEnumerable<T> items)
    {
        foreach (T item in items)
        {
            Console.WriteLine(item);
        }
    }
}
```

> **OUTPUT 15.6**
>
> Corporate
> Human Resources
> Engineering
> Information Technology
> Philanthropy
> Marketing
>
> Mark Michaelis (Chief Computer Nerd)
> Michael Stokesbury (Senior Computer Wizard)
> Brian Jones (Enterprise Integration Guru)
> Anne Beard (HR Director)
> Pat Dever (Enterprise Architect)
> Kevin Bost (Programmer Extraordinaire)
> Thomas Heavey (Software Architect)
> Eric Edmonds (Philanthropy Coordinator)

We use this data in the example in the following section on joining data.

## Performing an Inner Join with Join()

In the world of objects on the client side, relationships between objects are generally already set up. For example, the relationship between files and the directories in which they reside are preestablished with the `DirectoryInfo.GetFiles()` method and the `FileInfo.Directory` method, respectively. Frequently, however, this is not the case with data being loaded from nonobject stores. Instead, the data needs to be joined together so that you can navigate from one type of object to the next in a way that makes sense for the data.

Consider the example of employees and company departments. In Listing 15.19, we join each employee to his or her department and then list each employee with his or her corresponding department. Since each employee belongs to only one (and exactly one) department, the total number of items in the list is equal to the total number of employees—each employee appears only once (each employee is said to be normalized). Output 15.7 shows the results.

**LISTING 15.19: An Inner Join Using System.Linq.Enumerable.Join()**

```csharp
using System;
using System.Linq;

// ... 

Department[] departments = CorporateData.Departments;
Employee[] employees = CorporateData.Employees;

IEnumerable<(int Id, string Name, string Title, Department Department)> items =
    employees.Join(
        departments,
        employee => employee.DepartmentId,
        department => department.Id,
        (employee, department) => (
            employee.Id,
            employee.Name,
            employee.Title,
            department
    ));

foreach (var item in items)
{
    Console.WriteLine(
        $"{ item.Name } ({ item.Title })");
    Console.WriteLine("\t" + item.Department);
}

// ...
```

**OUTPUT 15.7**

```text
Mark Michaelis (Chief Computer Nerd)
    Corporate
Michael Stokesbury (Senior Computer Wizard)
    Engineering
Brian Jones (Enterprise Integration Guru)
    Engineering
Anne Beard (HR Director)
    Human Resources
Pat Dever (Enterprise Architect)
    Information Technology
Kevin Bost (Programmer Extraordinaire)
    Engineering
Thomas Heavey (Software Architect)
    Engineering
Eric Edmonds (Philanthropy Coordinator)
    Philanthropy
```

The first parameter for Join() has the name inner. It specifies the collection, departments, that employees joins to. The next two parameters are lambda expressions that specify how the two collections will connect: employee => employee.DepartmentId (with a parameter name of outerKeySelector) identifies that on each employee, the key will be DepartmentId. The next lambda expression (department => department.Id) specifies the Department's Id property as the key—in other words, for each employee, join a department where employee.DepartmentId equals department.Id. The last parameter is the resultant item that is selected. In this case, it is a tuple with Employee's Id, Name, and Title as well as a Department property with the joined department object.

Notice in the output that Engineering appears multiple times—once for each employee in CorporateData. In this case, the Join() call produces a Cartesian product between all the departments and all the employees such that a new record is created for every case where a record exists in both collections and the specified department IDs are the same. This type of join is an inner join.

The data could also be joined in reverse, such that department joins to each employee to list each department-to-employee match. Notice that the output includes more records than there are departments: There are multiple employees for each department, and the output is a record for each match. As we saw before, the Engineering department appears multiple times, once for each employee.

The code in Listing 15.20 (which produces Output 15.8) is similar to that in Listing 15.19, except that the objects, Departments and Employees, are reversed. The first parameter to Join() is employees, indicating what departments joins to. The next two parameters are lambda expressions that specify how the two collections will connect: department => department.Id for departments and employee => employee.DepartmentId for employees. As before, a join
