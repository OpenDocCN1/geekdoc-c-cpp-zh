# Constructors 345

the constructor with the most parameters, passing defaults for the parameters that are not known.

# BEGINNER TOPIC

# Centralizing Initialization

Notice that in the Employee(int id) constructor implementation in Listing 6.34, you cannot call this(firstName, lastName) because no such parameters exist on this constructor. To enable such a pattern, in which all initialization code happens through one method, you must create a separate method, as shown in Listing 6.35.

Listing 6.35: Providing an Initialization Method

```
public class Employee {
    // FirstName&LastName set inside Initialize() method.
    #pragma warning disable CS8618
    public Employee(string firstName, string lastName) {
        int id;
        // Generate an employee ID.
        // ...
        Initialize(id, firstName, lastName);
    }
    public Employee(int id, string firstName, string lastName) {
        Initialize(id, firstName, lastName);
    }
    public Employee(int id) {
        string firstName;
        string lastName;
        Id = id;
        // Look up employee data
        // ...
        Initialize(id, firstName, lastName);
    }
}
```