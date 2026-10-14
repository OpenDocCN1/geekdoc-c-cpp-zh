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
```