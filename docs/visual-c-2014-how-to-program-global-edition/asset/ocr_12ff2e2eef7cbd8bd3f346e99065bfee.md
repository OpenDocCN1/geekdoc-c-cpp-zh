# Contravariance in Arrays

Previously, we showed that an array of a derived-class type (salariedEmployees) can be assigned to an array variable of a base-class type (employees). Now, consider the following statement, which has always compiled in C#:

```
SalariedEmployee[] salariedEmployees2 =
(SalariedEmployee[]) employees;
```

Based on the previous statements, we know that the Employee variable employees currently refers to an array of SalariedEmployees. Using a cast operator to assign employees—an array of base-class type elements—to salariedEmployees2—an example of contravariance. The casting will fail at runtime if employees is not an array of salariedEmployees.

# Contravariance in Generic Types

To understand contravariance in generic types, consider a SortedSet of SalariedEmployees maintains a set of objects in sorted order—no duplicates are allowed. The objects placed in SortedSet implement the IComparable<T> interface. For classes that do not implement this interface, you can compare their objects using an object that implements the IComparable<T> interface. This interface's Compare method compares two values and returns 0, a negative integer if the first is less than the second, or a positive integer if the first is greater than the second.

Our Employee hierarchy do not implement IComparable<T>. Let's assume we want to sort Employees by social security number. We can implement the following class

```
class EmployeeComparer : IComparable<Employee>
{
    int IComparable<Employee>.Compare(Employee a, Employee b)
    {
        return a.SocialSecurityNumber.CompareTo(
            b.SocialSecurityNumber);
    }
}
```

Method Compare returns the result of comparing the two Employees' social security number using string CompareTo. Now consider the following statement, which creates a SortedSet:

```
SortedSet<SalariedEmployee> set =
new SortedSet<SalariedEmployee>(new EmployeeComparer());
```

When the argument does not implement IComparable<T>, you must supply an appropriate IComparer<T> to compare the objects that will be placed in the SortedSet. Since we are creating a SortedSet of SalariedEmployees, the compiler expects the IComparable<T> object to implement the IComparable<SalariedEmployee>. Instead, we provided an IComparer that implements IComparable<Employee>. The compiler allows you to provide an IComparer for a base-class type where an IComparer for a derived-class type is expected because interface IComparable<T> supports contravariance.