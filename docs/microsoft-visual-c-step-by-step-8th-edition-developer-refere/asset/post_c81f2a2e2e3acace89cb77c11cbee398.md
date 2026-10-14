
## Note

In contrast with SQL, the order of the expressions in the on clause of a LINQ expression is important. You must place the item you are joining from (referencing the data in the collection in the from clause) to the left of the equals operator and the item you are joining with (referencing the data in the collection in the join clause) to the right.

LINQ provides a large number of other methods for summarizing information and joining, grouping, and searching through data. This section has covered just the most common features. For example, LINQ provides the Intersect and Union methods, which you can use to perform set-wide operations. It also provides methods such as Any and All that you can use to determine whether at least one item in a collection or every item in a collection matches a specified predicate. You can partition the values in an enumerable collection by using the Take and Skip methods. For more information, see the material in the LINQ section of the documentation provided with Visual Studio 2015.

## Querying data in Tree<TItem> objects

The examples you’ve seen so far in this chapter have shown how to query the data in an array. You can use exactly the same techniques for any collection class that implements the generic IEnumerable<T> interface. In the following exercise, you will define a new class for modeling employees for a company. You will create a BinaryTree object containing a collection of Employee objects, and then you will use LINQ to query this information. You will initially call the LINQ extension methods directly, but then you will modify your code to use query operators.

## Retrieve data from a BinaryTree by using the extension methods

- 1. Start Visual Studio 2015 if it is not already running.
- 2. Open the QueryBinaryTree solution, which is located in the \Microsoft Press\VCSBS\Chapter 21\QueryBinaryTree folder in your Documents folder. The project contains the Program.cs file, which defines the Program class with the Main and doWork methods that you have seen in previous exercises.
- 3. In Solution Explorer, right-click the QueryBinaryTree project, point to Add, and then click Class. In the Add New Item – Query BinaryTree dialog box, type Employee.cs in the Name box, and then click Add.
- 4. Add the automatic properties shown in bold in the following code to the Employee class:

Click here to view code image

```
class Employee
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Department { get; set; }
    public int Id { get; set; }
}
```

5. Add the ToString method shown in bold in the code that follows to the Employee class. Types in the .NET Framework use this method when converting the object to a string representation, such as when displaying it by using the Console.WriteLine statement.

Click here to view code image

```
class Employee
{
    ...
    public override string ToString()
    {
        return
            $"Id: {this.Id}, Name: {this.FirstName}
{this.LastName}, Dept: {this.Department}";
    }
}
```

6. Modify the definition of the Employee class to implement the IComparable<Employee> interface, as shown here:

Click here to view code image

```
class Employee : IComparable<Employee>
{
}
```

This step is necessary because the BinaryTree class specifies that its elements must be “comparable.”

7. Hover over the IComparable<Employee> interface in the class definition, click the lightbulb icon that appears, and then click Implement Interface Explicitly on the context menu.

This action generates a default implementation of the CompareTo method. Remember that the BinaryTree class calls this method when it needs to compare elements when inserting them into the tree.

8. Replace the body of the CompareTo method with the following code shown in bold. This implementation of the CompareTo method compares Employee objects based on the value of the Id field.

Click here to view code image

```
int IComparable<Employee>.CompareTo(Employee other)
{
    if (other == null)
{
    return 1;
}

if (this.Id > other.Id)
{
    return 1;
}

if (this.Id < other.Id)
{
    return -1;
}

return 0;
}
```

## Note

For a description of the IComparable<T> interface, refer to Chapter 19.

- 9. In Solution Explorer, right-click the QueryBinaryTree solution, point to Add, and then click Existing Project. In the Add Existing Project dialog box, move to the folder Microsoft Press\VCSBS\Chapter 21\BinaryTree in your Documents folder, click the BinaryTree project, and then click Open. The BinaryTree project contains a copy of the enumerable BinaryTree class that you implemented in Chapter 19.
- 10. In Solution Explorer, right-click the QueryBinaryTree project, point to Add, and then click Reference. In the Reference Manager – QueryBinaryTree dialog box, in the left pane, click Solution. In the middle pane, select the BinaryTree project, and then click OK.
- 11. Display the Program.cs file for the QueryBinaryTree project in the Code and Text Editor window, and verify that the list of using directives at the top of the file includes the following line of code:
  
  using System.Linq;
- 12. Add the following using directive to the list at the top of the Program.cs file to bring the BinaryTree namespace into scope:
  
  using BinaryTree;
- 13. In the doWork method in the Program class, remove the // TODO: comment and add the following statements shown in bold to construct and populate an instance of the BinaryTree class:

Click here to view code image

```
static void doWork()
{
    Tree<Employee> empTree = new Tree<Employee>(
        new Employee { Id = 1, FirstName = "Kim", LastName = "Abercrombie", Department = "IT" });
    empTree.Insert(
        new Employee { Id = 2, FirstName = "Jeff", LastName = "Hay", Department = "Marketing" });
    empTree.Insert(
        new Employee { Id = 4, FirstName = "Charlie", LastName = "Herb", Department = "IT" });
    empTree.Insert(
        new Employee { Id = 6, FirstName = "Chris", LastName = "Preston", Department = "Sales"});
    empTree.Insert(
        new Employee { Id = 3, FirstName = "Dave", LastName = "Barnett", Department = "Sales" });
    empTree.Insert(
        new Employee { Id = 5, FirstName = "Tim", LastName = "Litton", Department="Marketing" });
}
```

14. Add the following statements shown in bold to the end of the doWork method. This code invokes the Select method to list the departments found in the binary tree.

Click here to view code image

```
static void doWork()
{
    ...
    Console.WriteLine("List of departments");
    var depts = empTree.Select(d => d.Department);

    foreach (var dept in depts)
    {
        Console.WriteLine($"Department: {dept}");
    }
}
```

15. On the Debug menu, click Start Without Debugging.

The application should output the following list of departments:

```
List of departments
Department: IT
Department: Marketing
Department: Sales
Department: IT
Department: Marketing
Department: Sales
```

Each department occurs twice because there are two employees in each department. The order of the departments is determined by the CompareTo method of the Employee class, which uses the Id property of each employee

to sort the data. The first department is for the employee with the Id value 1, the second department is for the employee with the Id value 2, and so on.

16. Press Enter to return to Visual Studio 2015.

17. In the doWork method in the Program class, modify the statement that creates the enumerable collection of departments as shown in bold in the following example:

Click here to view code image

```
var depts = empTree.Select(d => d.Department).Distinct();
```

The Distinct method removes duplicate rows from the enumerable collection.

18. On the Debug menu, click Start Without Debugging.

Verify that the application now displays each department only once, like this:

```
List of departments
Department: IT
Department: Marketing
Department: Sales
```

19. Press Enter to return to Visual Studio 2015.

20. Add the following statements shown in bold to the end of the doWork method. This block of code uses the Where method to filter the employees and return only those in the IT department. The Select method returns the entire row rather than projecting specific columns.

Click here to view code image

```
static void doWork()
{
    ...
    Console.WriteLine("\nEmployees in the IT department");
    var ITEmployees =
        empTree.Where(e => String.Equals(e.Department, "IT"))
        .Select(emp => emp);

    foreach (var emp in ITEmployees)
    {
        Console.WriteLine(emp);
    }
}
```

21. After the code from the preceding step, add the following code shown in bold to the end of the doWork method. This code uses the GroupBy method to group the employees found in the binary tree by department. The outer foreach statement iterates through each group, displaying the name of the department. The inner foreach statement displays the names of the
