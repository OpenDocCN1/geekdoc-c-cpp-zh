# Step-by-Step

Create a Person class with properties FirstName, LastName, Street, City, State, Zip, Email, and Phone. Give the Person class a GetAddress method that returns the Person's name and address properties as a string in the format:

Alice Archer
100 Ash Ave
Bugsville  CO  82010

+   1. Make a new Person class with code similar to the following:

```
class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Street { get; set; }
    public string City { get; set; }
    public string State { get; set; }
    public string Zip { get; set; }

    // Display the person's address.
    // A real application might print this on an envelope.
    public string GetAddress()
    {
        return FirstName + " " + LastName +
            "\n" + Street + "\n" + City +
            " " + State + " " + Zip;
    }
}
```

Derive an Employee class from Person. Add the properties EmployeeId and MailStop.

+   1. Make the Employee class similar to the following:

```
class Employee : Person
{
    public int EmployeeId { get; set; }
    public string MailStop { get; set; }
}
```

Derive a Manager class from Employee. Add a DepartmentName property and a DirectReports property of type List<Employee>. Make a GetDirectReportsList method that returns the names of the Manager's Employees separated by newlines.

+   1. Make the Manager class similar to the following:

```
class Manager : Employee
{
    public string DepartmentName { get; set; }
    public List<Employee> DirectReports = new List<Employee>();

    // Return a list of this manager's direct reports.
    public string GetDirectReportsList()
```