differs only in the case of the initial letter, and many organizations do precisely this.

If your organization follows this approach, you should be aware of one important drawback. Examine the following code, which implements a class named Employee. The employeeID field is private, and the EmployeeID property provides public access to this.

Click here to view code image

```
class Employee {
    private int employeeID;
    public int EmployeeID {
        get => this.EmployeeID;
        set => this.EmployeeID = value;
    }
}
```

This code will compile perfectly but results in a program raising a StackOverflowException whenever the EmployeeID property is accessed. The exception occurs rather than the get and set assessors reference the property (uppercase E) the private field (lowercase e), which triggers an endless recursive loop that eventually causes the process to exhaust the available memory. This type of bug is very difficult to spot! For this reason, the examples in this book name the private fields used to provide the data for properties with a leading underscore; it makes them much easier to distinguish from the names of properties. All other private fields will continue to use camelCase identifiers without a leading underscore.

# Using properties

When you use a property in an expression, you can use it in a read context (when you are retrieving its value) and in a write context (when you are modifying its value). The following example shows how to read values from the x and y properties of the ScreenPosition structure:

Click here to view code image

```
ScreenPosition origin = new ScreenPosition(0, 0);
int xpos = origin.X; // calls origin.get
```