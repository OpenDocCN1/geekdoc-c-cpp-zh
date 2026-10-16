```
{
    Type type = typeof(Customer);
    PropertyInfo[] propertyInfo = type.GetProperties();
    Console.WriteLine("The Customer class properties list is:--");
    foreach (PropertyInfo pInfo in propertyInfo)
    {
        Console.WriteLine(pInfo.Name);
    }
}
```

The method called GetProperties for the Type class will return an array of the PropertyInfo type, which lists the public properties for the type. This array can then be iterated and we can retrieve a name for each public property that has been defined in the type. Because three properties are defined in the Customer class, all three names would display in the console window on the execution of the window.

Below, the example shows how to use reflection to display the metadata for the public methods and the constructors of a specified type. Going back to the Customer class we defined earlier, we are going to add two new methods – a method named Validate used to validate the parameter, which is a customer object, and a default constructor. The new version of our Customer class should now look like this:

```
public class Customer
{
    public Customer()
    {
        //Default constructor
    }
    public int Id
```