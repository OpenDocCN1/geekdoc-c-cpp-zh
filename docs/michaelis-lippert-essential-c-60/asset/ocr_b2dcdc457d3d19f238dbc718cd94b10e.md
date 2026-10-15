# Instance Fields

One of the key aspects of object-oriented design is the grouping of data to provide structure. This section discusses how to add data to the Employee class. The general object-oriented term for a variable that stores data within a class is member variable. This term is well understood in C#, but the more standard term and the one used in the specification is field, which is a named unit of storage associated with the containing type. Instance fields are variables declared at the class level to store data associated with an object. Hence, association is the relationship between the field data type and the containing field.

# Declaring an Instance Field

In Listing 5.4, the class Employee has been modified to include three fields: FirstName, LastName, and Salary.

# LISTING 5.4: Declaring Fields

```
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary;
}
```

With these fields added, it is possible to store some fundamental data with every Employee instance. In this case, you prefix the fields with an access modifier of public. The use of public on a field indicates that the data within the field is accessible from classes other than Employee (see the section “Access Modifiers,” later in this chapter).

As with local variable declarations, a field declaration includes the data type to which the field refers. Furthermore, it is possible to assign fields an initial value at declaration time, as demonstrated with the Salary field in Listing 5.5.

# LISTING 5.5: Setting Initial Values of Fields at Declaration Time

```
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary = "Not enough";
}
```