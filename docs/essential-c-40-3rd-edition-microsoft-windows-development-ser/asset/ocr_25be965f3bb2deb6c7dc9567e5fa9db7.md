In Listing 5.9 and Listing 5.10, the this keyword is not used in the GetName() method—it is optional. However, if local variables or parameters exist with the same name as the field (see the SetName() method in Listing 5.10), then leaving off this would result in accessing the local variable/parameter rather than the field, so this would be required.

You can also use the keyword this to access a class's methods explicitly. this.GetName() is allowed within the SetName() method, for example, allowing you to print out the newly assigned name (see Listing 5.11 and Output 5.3).

# LISTING 5.11: Using this with a Method

```
class Employee
{
// ...

public string GetName()
{
return FirstName + " " + LastName;
}

public void SetName(string newFirstName, string newLastName)
{
this.FirstName = newFirstName;
this.LastName = newLastName;
Console.WriteLine("Name changed to \"{0}\"",
this.GetName());
}
}

class Program
{
static void Main()
{
Employee employee = new Employee();
employee.SetName("Inigo", "Montoya");
// ...
}
// ...
}
```